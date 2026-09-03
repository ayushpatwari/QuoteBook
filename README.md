# QuoteBook

QuoteBook is an iOS application for discovering, creating, organizing, and saving quotes. Built with **Swift and SwiftUI**, the app uses **Firebase Authentication and Cloud Firestore** for user accounts and cloud-backed data, with an **MVVM-style architecture** to separate application state, data access, and UI logic.

The project was designed as a full-featured mobile application rather than a static UI prototype, with authentication, persistent user data, quote discovery, search, likes, custom collections, and quote creation/editing.

## Features

* **Quote Discovery** — Browse quotes stored in Firestore and surface popular quotes based on likes.
* **Search** — Search discovered quotes by author.
* **Likes** — Like and unlike quotes with user-specific state persisted through Firebase.
* **Personal Library** — Maintain a library of saved and user-created quotes.
* **Quote Creation & Editing** — Create custom quotes with an author, color, visibility, and tags, and edit existing entries.
* **Collections** — Organize quotes into custom collections with configurable names and colors.
* **Authentication** — User authentication and session state backed by Firebase Authentication.
* **Multi-Page Navigation** — Navigate between Discover, Collections, and Library views through a custom tab-based interface.

## Tech Stack

| Technology                  | Usage                                                         |
| --------------------------- | ------------------------------------------------------------- |
| **Swift**                   | Core application logic                                        |
| **SwiftUI**                 | Declarative iOS user interface                                |
| **Firebase Authentication** | User authentication and session management                    |
| **Cloud Firestore**         | Cloud storage for quotes, users, likes, and collections       |
| **MVVM**                    | Separation of views, state, business logic, and data services |
| **Xcode**                   | Development and iOS application tooling                       |

## Architecture

QuoteBook follows an **MVVM-style architecture** to separate presentation logic from data access and application state.

```text
Views
  │
  ▼
ViewModels
  │
  ▼
Services / Data Layer
  │
  ▼
Firebase
```

### Views

SwiftUI views are responsible for rendering the interface and responding to user interactions.

Examples include:

* `DiscoverPage`
* `CollectionsView`
* `LibraryView`
* `AddQuoteView`
* `EditQuoteView`
* `LoginScreen`

### ViewModels

Observable view models expose application state to SwiftUI using properties such as `@Published`.

For example, the quote view model manages:

* discovered quote state
* author search
* date-based quote filtering
* liking and unliking quotes
* checking user-specific like state

### Services

Firebase operations are separated from the UI through service components. The quote service, for example, retrieves quotes from Firestore and updates their like counts.

This separation keeps database operations independent from the views and makes application behavior easier to maintain and extend.

## Firebase Data Flow

QuoteBook uses Firebase as its cloud backend.

A simplified flow looks like:

```text
SwiftUI View
     │
     ▼
 ViewModel
     │
     ▼
 Service
     │
     ▼
Cloud Firestore
```

User-specific data is associated with the authenticated Firebase user, allowing features such as liked quotes and collections to persist independently for each account.

## Project Structure

```text
QuoteBookApp/
├── CollectionsPage/
│   ├── Data/
│   └── Views/
│
├── DisoverPage/
│   ├── Model/
│   ├── Services/
│   ├── ViewModel/
│   └── Views/
│
├── LibraryAndQuoteMaker/
│   ├── Helpers/
│   └── Views/
│
├── ContentView.swift
├── HomePage.swift
├── tabModel.swift
└── QuoteBookAppApp.swift
```

The feature-based directory structure keeps models, services, view models, and views organized around their corresponding parts of the application.

## Quote Discovery

Quotes are retrieved from Cloud Firestore and ordered by popularity based on their number of likes.

The Discover feature also supports:

* author-based searching
* user-specific like state
* adding and removing quotes from a user's liked collection
* date-based filtering of quote content

## Collections

Users can create personalized collections by:

1. Choosing a collection name.
2. Selecting quotes to include.
3. Choosing a collection color.
4. Saving the collection.

Existing collections can also be updated or deleted.

## Creating Quotes

The quote creation interface supports:

* quote text
* author
* tags
* custom color
* public/private visibility

Input validation is used to prevent invalid quote content before submission.

## Getting Started

### Prerequisites

* macOS
* Xcode
* An iOS Simulator or physical iOS device
* A Firebase project configured for an iOS application

### Installation

Clone the repository:

```bash
git clone https://github.com/ayushpatwari/QuoteBook.git
cd QuoteBook
```

Open the Xcode project:

```bash
open QuoteBookApp.xcodeproj
```

Configure the project with the required Firebase credentials for your Firebase project, then build and run the application through Xcode.
