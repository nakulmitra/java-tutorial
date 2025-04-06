# Dummy Instagram Project

## Project Overview
This project is a simplified version of Instagram implemented in Java. The goal is to consolidate core Java concepts, including **Object-Oriented Programming (OOP)**, **Exception Handling**, and the **Stream API**, into a practical, hands-on application. The Dummy Instagram platform enables users to:
1. Create accounts with proper validation.
2. Add posts and view posts.
3. Like and comment on posts.
4. Interact with posts from other users.
5. View the overall state of all users and their posts.

This project serves as a foundation for understanding how to design and implement social media-like applications using Java.

[![](https://markdown-videos-api.jorgenkh.no/youtube/CFMyJaRCPwk)](https://youtu.be/CFMyJaRCPwk)

## Features
1. User Accounts
* Create user accounts with a username and email.
* Validate email format using custom exceptions.

2. Posts
* Users can add posts.
* Posts support likes and comments.
* Track the number of likes and display all comments.

3. Interactions
* Users can like or unlike posts.
* Users can comment on posts.

4. View System State
* Display all users and their respective posts, likes, and comments.

## Class Design
### 1. User Class
The `User` class represents an Instagram user.

**Attributes:**
* `username:` The user's name (unique).
* `email:` The user's email address (validated using a custom exception).
* `posts:` A list of the user's posts.

**Methods:**
* `addPost(String content):` Adds a new post to the user's list of posts.
* `getUsername():` Returns the user's username.
* `getPosts():` Returns the list of the user's posts.

### 2. Post Class
The Post class represents a user's post.

**Attributes:**
* `postId:` Unique ID for each post.
* `content:` Content of the post.
* `likes:` A map to track which users liked the post.
* `comments:` A list of comments on the post.

**Methods:**
* `toggleLike(String username):` Allows a user to like or unlike the post.
* `addComment(String commenter, String commentText):` Adds a comment to the post.
* `getLikeCount():` Returns the total number of likes.
* `getComments():` Returns the list of comments.
* `toString():` Formats the post details for display.

### 3. Comment Class
The Comment class represents a comment on a post.

**Attributes:**
* `commenter:` The username of the person who commented.
* `text:` The comment text.

**Methods:**
* `toString():` Formats the comment for display.

### 4. Custom Exception
The `InvalidEmailException` class is a custom exception used to validate email addresses.

**Usage:**
Thrown when an email does not contain the '@' symbol.

## Implementation
1. **User Class**
```
package com.devportal;

import java.util.ArrayList;
import java.util.List;

public class User {
	
	private String username;
	private String email;
	private List<Post> posts = new ArrayList<>();
	
	public User(String username, String email) throws InvalidEmailException {
		if(!email.contains("@")) {
			throw new InvalidEmailException("Invalid email format " + email);
		}
		
		this.username = username;
		this.email = email;
	}
	
	public void addPost(String content) {
		posts.add(new Post(posts.size() + 1, content));
		System.out.println("Post added: " + content);
	}
	
	public String getUsername() {
		return username;
	}
	
	public List<Post> getPosts(){
		return posts;
	}

}
```

2. **Post Class**
```
package com.devportal;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Post {
	
	private int postId;
	private String content;
	private Map<String, Boolean> likes = new HashMap<>(); // To track user like
	private List<Comment> comments = new ArrayList<>();
	
	public Post(int postId, String content) {
		this.postId = postId;
		this.content = content;
	}
	
	public void toggleLike(String username) {
		if(likes.containsKey(username) && likes.get(username)) {
			likes.put(username, false);
			System.out.println(username + " unliked the post!!!");
		}else {
			likes.put(username, true);
			System.out.println(username + " liked the post!!!");
		}
	}
	
	public void addComment(String commenter, String text) {
		comments.add(new Comment(commenter, text));
		System.out.println("Comment added by " + commenter + ": " + text);
	}
	
	public int getLikeCount() {
		return (int) likes.values().stream().filter(Boolean::booleanValue).count();
	}
	
	public List<Comment> getComments(){
		return comments;
	}
	
	@Override
	public String toString() {
		return "PostId: " + postId + ", Content: \"" + content + "\", Likes: " + getLikeCount() + ", Comments: " + comments.size(); 
	}

}
```

3. **Comment Class**
```
package com.devportal;

public class Comment {
	
	private String commenter;
	private String text;
	
	public Comment(String commenter, String text) {
		this.commenter = commenter;
		this.text = text;
	}
	
	@Override
	public String toString() {
		return commenter + ": " + text;
	}

}
```

4. **Custom Exception**
```
package com.devportal;

public class InvalidEmailException extends Exception {
	
	public InvalidEmailException(String msg) {
		super(msg);
	}
}
```

5. **Main Program**
The Main class ties everything together, simulating user interactions.

`Users can:`
* Choose to act as a specific user.
* Add posts.
* View all posts from all users.
* Like or comment on posts.

```
package com.devportal;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Scanner;

import javax.swing.plaf.basic.BasicComboBoxEditor;

public class Main {

	private static List<User> users = new ArrayList<>();

	public static void main(String[] args) {
		try {
			// Initial users
			User sahil = new User("Sahil", "sahil@example.com");
			User aman = new User("Aman", "aman@example.com");

			sahil.addPost("Sahil's first post");
			sahil.addPost("Loving java tutorial in Dev Portal");
			aman.addPost("My first post");

			users.add(sahil);
			users.add(aman);

			// User Interaction
			Scanner scanner = new Scanner(System.in);
			while (true) {
				System.out.println("===Welcome to Dummy Instagram===");
				System.out.println("1. Chose User");
				System.out.println("2. Display All users & their posts");
				System.out.println("3. Exit");
				System.out.println("Please enter your choice: ");
				int choice = scanner.nextInt();

				switch (choice) {
				case 1:
					System.out.println("\nAvailable Users: ");
					for (int i = 0; i < users.size(); i++) {
						System.out.println((i + 1) + ". " + users.get(i).getUsername());
					}

					System.out.println("Select a user by number");
					int userChoice = scanner.nextInt();

					if (userChoice < 1 || userChoice > users.size()) {
						System.out.println("Invalid User choice!!!");
						break;
					}

					User selectedUser = users.get(userChoice - 1);
					handleUserOperations(selectedUser, scanner);
					break;

				case 2:
					displayAllUsersAndPosts();
					break;

				case 3:
					System.out.println("Thank you for using Dummy Instagram!!!");
					scanner.close();
					return;

				default:
					System.out.println("Invalide Choice. Please try again!!!");
				}

			}
		} catch (InvalidEmailException e) {
			System.out.println(e.getMessage());
		}
	}

	private static void displayAllUsersAndPosts() {
		System.out.println("\n===All Users with their Post===");
		for (User user : users) {
			System.out.println("\nUser: " + user.getUsername());
			System.out.println("Post: ");
			for (Post post : user.getPosts()) {
				System.out.println(" - " + post);
				System.out.println(" Comments: ");

				for (Comment comment : post.getComments()) {
					System.out.println(" - " + comment);
				}
			}
		}
	}

	private static void handleUserOperations(User user, Scanner scanner) {
		while (true) {
			System.out.println("\n===Operations for " + user.getUsername() + "===");
			System.out.println("1. Add Post");
			System.out.println("2. View All Post");
			System.out.println("3. Go back");
			System.out.println("Please enter your choice: ");
			int choice = scanner.nextInt();
			scanner.nextLine(); // Consume next line

			switch (choice) {
			case 1:
				System.out.println("Please enter post content: ");
				String content = scanner.nextLine();
				user.addPost(content);
				break;

			case 2:
				interactWithAllPost(user, scanner);
				break;

			case 3:
				return;

			default:
				System.out.println("Invalid choice. Please try again!!!");
			}
		}
	}

	private static void interactWithAllPost(User user, Scanner scanner) {
		List<Post> allPosts = new ArrayList<>();
		Map<Integer, Post> postMap = new HashMap<>();

		System.out.println("===All Posts===");
		int index = 1;

		for (User u : users) {
			for (Post post : u.getPosts()) {
				allPosts.add(post);
				postMap.put(index, post);
				System.out.println(index + ". [" + u.getUsername() + "] " + post);
				index += 1;
			}
		}

		if (allPosts.isEmpty()) {
			System.out.println("No post available to intract with.");
			return;
		}

		System.out.println("\nSelect a post by number to intrect with (or enter 0 to go back)");
		int postChoice = scanner.nextInt();
		scanner.nextLine(); // Consume next line

		if (postChoice == 0) {
			return;
		}

		Post selectedPost = postMap.get(postChoice);
		if (null == selectedPost) {
			System.out.println("Invalid post choice!!!");
			return;
		}

		System.out.println("\n===Interact with Post===");
		System.out.println("1. Like/Unlike post");
		System.out.println("2. Comment on post");
		System.out.println("3. Go back");
		System.out.println("Please enter your choice: ");
		int actionChoice = scanner.nextInt();
		scanner.nextLine(); // Consume next line

		switch (actionChoice) {
		case 1:
			selectedPost.toggleLike(user.getUsername());
			break;

		case 2:
			System.out.println("Enter your comment: ");
			String comment = scanner.nextLine();
			selectedPost.addComment(user.getUsername(), comment);
			break;

		case 3:
			return;

		default:
			System.out.println("Invalid choice. Please try again!!!");
		}

	}
}
```

## Sample Output
1. Create users: Sahil and Aman.
2. Add posts.
3. Like and comment on posts.
4. Display all users and their posts with likes and comments.

## Potential Enhancements
* `Profile Updates:` Add functionality for users to update their profile information.
* `Follow/Unfollow System:` Allow users to follow or unfollow others.
* `Notifications:` Notify users when someone likes or comments on their posts.
* `Database Integration:` Use MySQL or MongoDB for persistent data storage.
* `RESTful API:` Expose functionality through APIs using frameworks like Spring Boot.
* `User Interface:` Implement a UI using Angular/React framework.

## Key Takeaways
* `Object-Oriented Programming:` Classes and methods are modular and reusable.
* `Exception Handling:` Ensures robust validation and error management.
* `Stream API:` Used for efficient data processing (likes, filtering, etc.).

## Conclusion
This Dummy Instagram project is a practical way to apply fundamental and advanced Java concepts. It provides a starting point for building more complex applications and learning about real-world system design. Explore the code, try the enhancements, and take your Java skills to the next level!

