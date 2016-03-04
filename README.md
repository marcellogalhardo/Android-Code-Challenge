Hi, guys. What's up?

# Description

Create an Android application that displays information received over the network.

1. Retrieve and print out the data received from the url above.
2. Parse the data retrieved from the server into a list of Java objects
3. Display your objects in an organized fashion (ListView, GridView, etc.)
  - Should display the name, city, state, and end date
4. In addition the object’s **name**, have your view display the image located at each object’s **icon** url.

# Implementation Details

To maintain the quality of good code, I decided to use an architecture based on the MVP pattern and inspired by the Clean / Hexagonal Architecture.

Basically I created three main packages: Core, Data and Ui.

![Clean / Hexagonal Architecture][architecture]

- Core: Keep the domain rules (which in this case are none), models and aggregations models.
- Date: Responsible for any data used in the application. Uses the Repository pattern.
- Ui: Responsible views. It is also responsible for the presentation (Presenter).

Obs: **Where is the Interactors in Core Layer?** I did not think it was necessary. I wanted to show my skills, but still want to keep as simple as possible.

### Repository Pattern
 
Allow change data from the internet and database without breaking the abstraction defined by the interface. Thus the code that uses the repository does not need to care about the place that the data is coming.

![Repository Pattern][repository_pattern]

### Model View Presenter

With the separation between View and Presenter, we create a isolated place for Unit Test and single responsibility layers. The Presenter allow unit test without the discomfort of mock Android SDK.

![Model View Presenter][mvp]

### UX / UI

I tried to follow the Material Design pattern in available time. Did you like it?

![Guide List][app]

### Libraries

1. RxJava + RxAndroid: This is the best way to work asynchronously and maintain the application scalable. I'm not a genius with Rx, but I really love it.
2. Retrofit + OkHttp: For Network Request and Rx integration.
3. Picasso: For image loading.
4. ButterKnife: For view binding.
5. PaperDb: For easy caching (database).
6. Gson: Retrofit integration for deserialize.

# Infraestruture Details

The server at the following url responds with JSON formatted data:

```(GET) http://guidebook.com/service/v2/upcomingGuides/```

The response represents a list of “Guide” objects:

```json
{
  "data": [
  {
    "startDate": "<date>",
    "endDate": "<date>",
    "name": "<name>",
    "url": "<url>",
    "venue": {"city": "<city>", "state": "<state>"},
    "icon": "<url to png image>"
    },
    … <more objects>
    ]
  }
  ```