### HW 1
Imagine you are a software developer at a large company and your team is developing a social media app to compete with X (formerly: Twitter). 

Write 5 user stories that capture the most important requirements for such a system. 

Please follow the common format (1 pts each) and list at least two acceptance criteria for each user story (1 pts each).
For each user story, justify how it satisfies each criteria of the INVEST Principle (3 pts each). 

Independent: Should be self-contained in a way that allows to be released without depending on one another.
Negotiable: Only capture the essence of user's need, leaving room for design decisions.
Valuable: Delivers value to end user.
Estimable: Developers should be able to estimate the effort it takes to implement the user story
Small: A user story is a small chunk of work that allows it to be completed in about 3 to 4 days.
Testable: A user story has to be confirmed via pre-written acceptance criteria

****

As a social media user, I want to be able to share text posts so that other users can view them.

Acceptance criteria:
1.) Given that a user has an account, when they upload content to the social media app, it appears on other users' apps so that it can be viewed from other accounts.
2.) Given that a user has created a post, when they choose to delete it from the app, it no longer appears on any other user's app and can no longer be viewed.

Independent: The only feature this relies on is having an account, and is independent of all other user stories.

Negotiable: There are no specifications about how the post should be displayed (design) or how it should be implemented.

Valuable: This is valuable to the user and other users on the app because creating and sharing content through posts would be the main way to interact with the app.

Estimable: Only one type of post (text), is implemented, so it is an estimable amount of effort for developers.

Small: Creating text posts cannot be broken up into smaller user stories, and it is a small self-contained feature that should be quick to implement.

Testable: The acceptance criteria defines cases where an implementation does not meet the requirements, for example, a user will not be able to upload a post if they do not have an account. Other users should not be able to view a deleted post. It would also not meet the criteria if a user posts but it can only be seen on the user's account and not by other users.

=====

As a content creator, I want to be able to see how many people liked my posts so that I can tell what type of content is most popular.

Acceptance criteria:
1.) Given that a certain number of users liked the post, when any user views the post then there should be a like count.

2.) Given that there is a post that other users can see, when any user likes the post then the like count should be updated.

Independent: Does not rely on any other features, other than posts. This is independent of comments.

Negotiable: Focuses on the idea of having "likes" but doesn't control how it is implemented or displayed. All that is requested is a way for other users and the original poster to see how the number of users that pressed the like button. 

Valuable: This is valuable because it allows content creators to get feedback on their posts.

Estimable: Developers can estimate the effort it would take to implement likes, as it only involves adding it to the UI, storing likes, updating and counting them.

Small: Feature is small and self-contained, involving all aspects that make the feature valuable, like for users to be able to input likes and for other users to see the number of likes.

Testable: The acceptance criteria defines how the feature should work and is easily testable. According to the acceptance criteria, the requirements are not satisfied if the number of likes does not update when someone likes the post, or if when a user views the post the like count is not updated or shown. This ensures that they are public and aren't just a hidden counter that users cannot gain value from.

=====

As a social media user, I want to be able to write comments under posts so that I can respond and communicate with other users.

Acceptance criteria:
1.) Given that a post exists, when a user uploads a comment, then it should appear under the post.

2.) Given that comments exist on a post, when a user replies to another user's comment, the comment should appear under the original message and in chronological order.

Independent: Separate from likes, though it depends on posts.

Negotiable: Doesn't specify exactly how they should be displayed or interacted with, just that users can add them and they should show up in a way that is intuitive for users to understand when they were posted (chronologically).

Valuable: Allows users to communicate directly and discuss the post with each other, which is valuable for users who are on the social media app who want to interact with other users while not wanting to create a post.

Estimable: Similar to posts, but just as text attached to a post, developers can get a good idea of how much effort it takes to implement it.

Small: Feature is small and self-contained, apart from posts. Only involves appending text below a post with fewer UI elements and containing just enough to make comments function the way they should - posting and replying (doesn't involve more complicated features like likes and reposts on comments)

Testable: The two acceptance criteria are the main testable requirements for comments. We want to test that the comment appears and that you can reply to it, and that they are public for all users to see. If a user posts a comment but it is not associated with the correct post, this would not satisfy the acceptance criteria. Also, if a user replies to a comment, it should be shown below the root comment for clarity, so if replies are shown out of order, it would not satisfy the acceptance criteria.

=====

As a social media user I want to be able to subscribe to another user so that I can receive notifications when that user posts new content.

Acceptance criteria:
1.) Given that a user has an account and is not subscribed to another given account, when the user chooses to subscribe to the account, then the user will be able to start receiving notifications when that account creates a new post.

2.) Given that a user is subscribed to another given account, when that account creates a new post, the user will receive a notification from the app and the user will be able to view the post using the notification.

Independent: This feature only depends on the posts feature and the implementation of user accounts. It is completely separate from comments, likes, and messages.

Negotiable: The user story specifies what should happen in different cases when the feature is implemented, but doesn't specify design choices (what should the button look like, what it should be called, etc.) or how the notifications should be implemented.

Valuable: Having this subscription/follower system allows users to better personalize their experience by seeing content that they actively choose to engage with and care about, which is valuable for the user.

Estimable: The effort to implement this feature is estimable because it should only involve tracking and updating the list of subscribed accounts for each user, implementing the notification system, and then updating the UI.

Small: The feature is self-contained and is the smallest user story that still provides value. It can easily be implemented after posts without affecting or overlapping with other features.

Testable: The feature is easily testable by checking the acceptance criteria. By subscribing and checking for notifications following a post, and also making sure that you don't receive notifications when not subscribed, will help test for the edge cases and ensure the feature is implemented correctly.

=====

As a social media user I want to be able to set a unique username so that I can customize my profile and so that other users can recognize me.

Acceptance criteria: 
1.) Given that a user has an account, when they choose to set a username that is not already in use, then that chosen name will display on their profile and be public to other users.

2.) Given that a user has a specific username, when another user tries to set that same username as their own, the app will show that the username is taken and recommends them to choose a new username.

Independent: Usernames are a feature that are completely independent of posts, comments, and likes and can be tested independently because there is no overlap. Users can have usernames without posts and vice versa.

Negotiable: There are few specifications on how the usernames or messages are to be displayed, or how usernames are to be stored and accessed, or what kind of restrictions there are on usernames.

Valuable: A unique username allows a user to personalize their profile on the app and makes it easier for other users to recognize their posts and search for them. 

Estimable: Developers should be able to estimate how much effort it will take to implement this, as the username system will only need to involve a way to store all users' usernames with the user's ID, checking for duplicates, and updating user data when they set their username.

Testable: These acceptance criteria can be tested easily by making an account, attempting to set the username and checking that it updates properly, and also attempting to set the username to an already existing username (which should fail).