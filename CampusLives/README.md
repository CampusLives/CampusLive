Original App Design Project - README Template
===

# CampusLive

## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)
2. [Schema](#Schema)

## Overview
### Description
Allows college students to share news, resources and events within the college.

### App Evaluation
- **Category: News/ Social Networking**
- **Mobile: This app would be primarily developed for IOS mobile **
- **Story: Users would be the students of a campus. The user can post the news and events going on campus.**
- **Market: Only students of a campus could choose to use this app, and to keep it a safe environemnt, students would need to verify their college email address.**
- **Habit: The app could be used as often as the user wants depending on the news and events going on cmapus**
- **Scope:First we would start with the students to share the news among their friends on campus, then perhaps this could evolve into a news sharing application among neighbourhoods to broaden its usage.**

## Product Spec

### 1. User Stories (Required and Optional)

**Required Must-have Stories**

* [User can login.]
* [User can sign up.]
* [User can follow/unfollow other users.]
* [User can post news]
* [User can verify news]
* [User can post a comment]

**Optional Nice-to-have Stories**

* [User can share a location.]
* [User can search for campus events.]
* [User can create groups.]


### 2. Screen Archetypes

* [Login]
   * [user can sign in.]
* [Register]
   * [User signs up a new account.]
* [Stream]
   * [Focus on primary context that user consumes in app]
* [Detail]
   * [Display all relevant information about single discrete item.]
* [Creation]
   * [Allow user to create new posts by presenting user with input fields and allowing them to attach media.]
* [Settings]
   * [Gives user the ability to tune preferences and profile setting associated with their account such as username and email]

### 3. Navigation

**Tab Navigation** (Tab to Screen)

* [News feed]
* [Search user]
* [Settings]
* [Post news]

**Flow Navigation** (Screen to Screen)

* [Login Screen]
* [Registration screen]
* [Stream screen]
* [Search Screen]
* [Detail Screen]
* [Creator Screen]

## Wireframes
<img src="https://github.com/CampusLives/CampusLive/blob/main/CampusLives/wireframes.png" width=600>

### [BONUS] Digital Wireframes & Mockups

### [BONUS] Interactive Prototype

## Schema 

### Models
Model: Users
**Property**|**Type**|**Description**
:-----:|:-----:|:-----:
UserId|String|Unique id for the user 
First name|String|First name of the user
Last name|String |Last name of the user
College Email|String|College email address of the user 

Model: Posts
**objectId**|**String**|**Unique id for the user post**
:-----:|:-----:|:-----:
author|Pointer to user|Image author
news|String |News by author
commentsCount|Number|Number of comments that has been posted to the posted news
verifyCount|Number|Number of verifications for the news
createdAt|DateTime|Date when news is created
updatedAt|DateTime|Date when news is last updated

### Networking
- Stream Screen:
    - (Read/GET) Query all posts where user is author
    ```swift
        // iOS
        // (Read/GET) Query all posts where user is author
        let query = PFQuery(className:"Post")
        query.whereKey("author", equalTo: currentUser)
        query.order(byDescending: "createdAt")
        query.findObjectsInBackground { (posts: [PFObject]?, error: Error?) in
           if let error = error {
              print(error.localizedDescription)
           } else if let posts = posts {
              print("Successfully retrieved \(posts.count) posts.")
            // TODO: Do something with posts...
          }
       }
    ```
    - (Create/POST) Create a new verify on a post
    -  (Delete) Delete existing verify
    - (Create/POST) Create a new comment on a post
    - (Delete) Delete existing comment
```swift
// Delete a Comment
PFObject.deleteAll(inBackground: objectArray) { (succeeded, error) in
    if (succeeded) {
        // The array of objects was successfully deleted.
    } else {
        // There was an error. Check the errors localizedDescription.
    }
}
```

- Creation Screen:
    -   (Create/POST) Create a new post object
    ```swift
    let posts = PFObject(className:"Post")
    posts["userId"] = 1337
    posts["First name"] = "Sean"
    posts.saveInBackground { (succeeded, error)  in
        if (succeeded) {
        // The object has been saved.
        } else {
        // There was a problem, check error.description
        }
    }
    ```

- Search Screen:
    - (Read/GET) Query all posts related to search field

- Detail Screen:
    - (Read/GET) Query all details of the post upon clicking the post
    - (Create/POST) Create a new verify on a post
    - (Delete) Delete existing verify
    - (Create/POST) Create a new comment on a post
    - (Delete) Delete existing comment
- Setting Screen:
    - (Read/GET) Query logged in user object
    - (Update/PUT) Update username, email, and password.
    ```swift
    let query = PFQuery(className:"User")
       query.getObjectInBackground(withId: "xWMyZEGZ") { (User: PFObject?, error: Error?) in
    if let error = error {
          print(error.localizedDescription)
    } else if let User = User {
         User["UserId"] = 1345
         User["email"] = sam@gmail.com
         User.saveInBackground()
    }
    }
    ```





