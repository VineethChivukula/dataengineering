# Data Vault Modeling

I will not go deep into the details of Data Vault modeling because there is just so much to cover and even I don't know it all. I will just cover what I know and what I have learned from my experience. If you want to learn more about it, go search for "Data Vault 2.0" on the internet.

On a high level Data Vault modeling is based on the idea of separating the data into three different types of tables: Hubs, Links, and Satellites.

- **Hubs:** Hubs are the central tables that contain the unique business keys. They are also used for storing the metadata about the business keys. Hubs are the only tables that can have a primary key, and they are also the only tables that can have a surrogate key.
- **Links:** Links are the tables that contain the relationships between the Hubs. They are used to connect the Hubs together and to store the metadata about the relationships. Links can have a composite primary key, which is made up of the surrogate keys from the Hubs that they connect.
- **Satellites:** Satellites are the tables that contain the descriptive attributes. They are used to store the historical data about the business keys. Satellites can have a composite primary key, which is made up of the surrogate key from the Hub and a timestamp.

```mermaid
flowchart TD
Hub1:::hub --> Link1:::link
Hub2:::hub --> Link1
Hub3:::hub --> Link1
Link1 --> Satellite1:::satellite

classDef hub stroke:#ff0;
classDef link stroke:#f0f;
classDef satellite stroke:#0ff;
```

You often hear about "Raw Vault" and "Business Vault". The Raw Vault is the initial stage of the Data Vault, where the data is loaded from the source systems into the Hubs, Links, and Satellites. The Business Vault is the stage where the data is transformed and enriched to create a more business-friendly version of the data. Also, instead of ids, we use "HK" (Hash Key) for the primary keys.

The main advantage of Data Vault modeling is that it allows for a high degree of flexibility and scalability. It also allows for a high degree of data quality and consistency, as the Hubs and Links are designed to be immutable. This means that once a record is inserted into a Hub or Link, it cannot be updated or deleted. This allows for a high degree of traceability and auditability, as all changes to the data are recorded in the Satellites.

I just recently created all these hubs, links, and satellites from scratch to satisfy client's new requirement, so that is why I am able to share this knowledge with you.

Let me show you a simple example of a Data Vault model for a social media usage analysis that needs to show latest data based on the recent date. The final report should show the username, user age, post content, post date, and platform name:

```mermaid
---
title: Social Media Usage Analysis Data Vault Model
---

classDiagram
class H_USER {
user_hk
load_date
}

class H_POST {
post_hk
load_date
}

class H_PLATFORM {
platform_hk
load_date
}

class L_USER_POST {
user_hk
post_hk
load_date
}

class L_POST_PLATFORM {
post_hk
platform_hk
load_date
}

class S_USER {
user_hk
user_name
user_email
user_age
user_gender
load_date
}

class S_POST {
post_hk
post_content
post_date
load_date
}

class S_PLATFORM {
platform_hk
platform_name
platform_category
platform_description
platform_url
load_date
}

class F_SOCIAL_MEDIA_USAGE_ANALYSIS {
user_hk
post_hk
platform_hk
}

class D_USER{
user_hk
user_name
user_email
user_age
load_date
}

class D_POST {
post_hk
post_content
post_date
load_date
}

class D_PLATFORM {
platform_hk
platform_name
platform_description
load_date
}

class REP_SOCIAL_MEDIA_USAGE_ANALYSIS {
user_hk
post_hk
platform_hk
user_name
user_age
post_content
post_date
platform_name
}

H_USER <|-- L_USER_POST : user_hk
H_POST <|-- L_USER_POST : post_hk
H_POST <|-- L_POST_PLATFORM : post_hk
H_PLATFORM <|-- L_POST_PLATFORM : platform_hk
H_USER <|-- S_USER : user_hk
H_POST <|-- S_POST : post_hk
H_PLATFORM <|-- S_PLATFORM : platform_hk

L_USER_POST <|-- F_SOCIAL_MEDIA_USAGE_ANALYSIS : user_hk, post_hk
L_POST_PLATFORM <|-- F_SOCIAL_MEDIA_USAGE_ANALYSIS : post_hk, platform_hk

H_USER <|-- D_USER : user_hk
S_USER <|-- D_USER : user_hk
H_POST <|-- D_POST : post_hk
S_POST <|-- D_POST : post_hk
H_PLATFORM <|-- D_PLATFORM : platform_hk
S_PLATFORM <|-- D_PLATFORM : platform_hk

S_USER <|-- F_SOCIAL_MEDIA_USAGE_ANALYSIS : user_hk
S_POST <|-- F_SOCIAL_MEDIA_USAGE_ANALYSIS : post_hk
S_PLATFORM <|-- F_SOCIAL_MEDIA_USAGE_ANALYSIS : platform_hk

D_USER <|-- REP_SOCIAL_MEDIA_USAGE_ANALYSIS : user_hk
F_SOCIAL_MEDIA_USAGE_ANALYSIS <|-- REP_SOCIAL_MEDIA_USAGE_ANALYSIS : user_hk
D_POST <|-- REP_SOCIAL_MEDIA_USAGE_ANALYSIS : post_hk
F_SOCIAL_MEDIA_USAGE_ANALYSIS <|-- REP_SOCIAL_MEDIA_USAGE_ANALYSIS : post_hk
D_PLATFORM <|-- REP_SOCIAL_MEDIA_USAGE_ANALYSIS : platform_hk
F_SOCIAL_MEDIA_USAGE_ANALYSIS <|-- REP_SOCIAL_MEDIA_USAGE_ANALYSIS : platform_hk

H_USER <|-- F_SOCIAL_MEDIA_USAGE_ANALYSIS : user_hk
```

Alright, I can guess the expression on your face right now haha. This is nothing, I swear to god there are way more links and satellites in my project.
