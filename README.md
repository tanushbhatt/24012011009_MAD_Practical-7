# Practical 7 — JSON API, HttpURLConnection & SQLite

### AIM

Develop an Android application that retrieves person data in **JSON format from an internet API** and stores the retrieved data in an **SQLite database**.

---

## 🎯 Practical Objective

This practical demonstrates how an Android application can:

1. Generate and use a JSON API URL.
2. Retrieve JSON data from the Internet.
3. Communicate with a web URL using `HttpURLConnection`.
4. Parse JSON data into `Person` objects.
5. Display person records using a `RecyclerView` adapter.
6. Store retrieved records in an SQLite database.
7. Read records from SQLite and display them in the application.
8. Delete a person record from both the database and the displayed list.
9. Use `Serializable` with the `Person` class as required by the practical.

---

## 🧠 Concepts Studied

- JSON Format
- JSON Parsing
- RecyclerView
- RecyclerView Adapter
- HttpURLConnection
- SQLite Database
- SQLiteOpenHelper
- ContentValues
- Cursor
- Internet Permission
- Serializable
- Background thread for network communication

---

## 🛠️ Technology Used

| Technology | Purpose |
|---|---|
| Kotlin | Application programming |
| XML | User interface |
| Android Studio | Development environment |
| RecyclerView | Displaying person records |
| SQLite | Local data storage |
| HttpURLConnection | Communicating with the web API |
| JSON | Data interchange format |

---

## 🌐 JSON API

The practical uses **JSON Generator** to create the person data API.

**JSON Generator:**  
https://app.json-generator.com/

**Generated API URL:**  
`https://api.json-generator.com/templates/5rDXHcbgpo93/data`

> **Security note:** The API token is intentionally not included in this README. Do not publish a private API token in a public GitHub repository.

The JSON data contains fields such as:

```text
id
email
phone
profile
    ├── name
    ├── address
    └── location
         ├── lat
         └── long
```

---

## 📄 Example JSON Structure

```json
[
  {
    "id": "example-id",
    "email": "example@gnu.ac.in",
    "phone": "+91 0000000000",
    "profile": {
      "name": "Example Person",
      "address": "Example Address",
      "location": {
        "lat": 19.123456,
        "long": 72.123456
      }
    }
  }
]
```

---

## 🔄 Application Flow

```text
JSON API URL
     ↓
HttpRequest
     ↓
HttpURLConnection
     ↓
Receive JSON Response
     ↓
JSON Parsing
     ↓
Person Objects
     ↓
SQLite Database
     ↓
Read Data from SQLite
     ↓
RecyclerView
     ↓
Display Person Records
```

---

## 🖥️ User Interface

The application displays person information in individual cards.

Each card contains:

- Person name
- Phone number
- Email ID
- Address
- Person icon
- Delete button

The practical output demonstrates both **Light Mode** and **Dark Mode** interfaces.

---

## 🗃️ SQLite Database

The application uses SQLite to store the retrieved person information locally.

### Database

```text
persons.db
```

### Table

```text
persons
```

### Columns

| Column | SQLite Type | Purpose |
|---|---|---|
| `id` | TEXT | Unique person ID |
| `person_name` | TEXT | Person name |
| `person_email_id` | TEXT | Email ID |
| `person_phone_no` | TEXT | Phone number |
| `person_address` | TEXT | Address |
| `person_lat` | REAL | Latitude |
| `person_long` | REAL | Longitude |

---

## 🧩 Main Files

```text
app/
└── src/
    └── main/
        ├── AndroidManifest.xml
        │
        ├── java/
        │   └── com.example.a24012011009_mad_practical_7/
        │       ├── MainActivity.kt
        │       ├── Person.kt
        │       ├── PersonAdapter.kt
        │       ├── PersonDbTableData.kt
        │       ├── DatabaseHelper.kt
        │       └── HttpRequest.kt
        │
        └── res/
            ├── drawable/
            │   ├── bg_avatar_circle.xml
            │   ├── bg_delete_circle.xml
            │   ├── bg_fab_rounded.xml
            │   ├── ic_delete.xml
            │   ├── ic_person.xml
            │   └── ic_refresh.xml
            │
            ├── layout/
            │   ├── activity_main.xml
            │   └── item_person.xml
            │
            ├── values/
            │   ├── colors.xml
            │   └── strings.xml
            │
            └── values-night/
                └── colors.xml
```

---

## 🧱 File Responsibilities

### `MainActivity.kt`

Controls the main screen and application flow.

It:

- Initializes the RecyclerView.
- Loads existing records from SQLite.
- Calls the HTTP request.
- Parses JSON data.
- Stores retrieved data in SQLite.
- Displays database records in the RecyclerView.
- Handles refresh and delete operations.

### `Person.kt`

Defines the `Person` model:

```text
id
name
emailId
phoneNo
address
latitude
longitude
```

The class implements `Serializable` as required by the practical.

### `PersonAdapter.kt`

Acts as the RecyclerView adapter.

It:

- Creates person card views.
- Displays person information.
- Updates the RecyclerView when data changes.
- Handles the delete button.

### `PersonDbTableData.kt`

Contains the SQLite table name, column names, and the SQL `CREATE TABLE` statement.

### `DatabaseHelper.kt`

Handles SQLite database operations such as:

- Database creation
- Table creation
- Insert
- Insert multiple records
- Read/query
- Delete
- Clear records
- Count records

A `Cursor` is used to read records from SQLite.

### `HttpRequest.kt`

Handles communication with the JSON web URL using:

```text
HttpURLConnection
```

It sends a `GET` request and converts the response stream into a String.

### `activity_main.xml`

Defines the main application screen containing:

- Screen title
- RecyclerView
- ProgressBar
- Empty-state message
- Refresh button

### `item_person.xml`

Defines the layout of one person card.

---

## 📥 Data Retrieval Process

When the application starts:

1. It checks whether person records already exist in SQLite.
2. If records exist, they are loaded and displayed.
3. Otherwise, the application requests JSON data from the Internet.
4. The JSON response is parsed.
5. The parsed person records are inserted into SQLite.
6. The application reads the records back from SQLite.
7. The records are displayed in the RecyclerView.

---

## 🗑️ Delete Operation

When the user presses the delete button:

```text
Delete Button
     ↓
Delete record from SQLite
     ↓
Remove item from RecyclerView
     ↓
Show Toast message
```

This keeps the displayed list synchronized with the database.

---

## 🔐 AndroidManifest Permission

Internet permission is added so the application can communicate with the JSON API:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

The practical also includes:

```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

---

## 🎨 Light & Dark Mode

The application provides separate color resources for normal and night mode.

```text
res/
├── values/
│   └── colors.xml
│
└── values-night/
    └── colors.xml
```

The same application UI can therefore adapt to the device's selected theme.

---

## ▶️ How to Run

1. Open the project in **Android Studio**.
2. Connect an Android device or start an emulator.
3. Make sure Internet permission is present in `AndroidManifest.xml`.
4. Configure your generated API URL and token in the application code.
5. Build the project.
6. Run the application.
7. The application retrieves person data from the JSON API.
8. Retrieved records are stored in SQLite and displayed in the RecyclerView.

---

## 📸 Screenshots

<table>
  <tr>
    <td><img width="401" height="872" alt="image" src="https://github.com/user-attachments/assets/69c4c28c-73f8-45f2-a6b3-fcbbdb701251" /></td>
    <td><img width="380" height="872" alt="image" src="https://github.com/user-attachments/assets/64570a14-ab76-4a0a-b32f-40d35f7091f6" /></td>
  </tr>
</table>
<img width="1817" height="577" alt="image" src="https://github.com/user-attachments/assets/1d570c38-384d-4cd6-8a64-ee54d45e72cd" />


---

## ✅ Expected Output

The application displays multiple person records retrieved from the JSON API.

Each record shows the person's:

```text
Name
Phone
Email
Address
```

The retrieved records are also stored in the local SQLite database, where they can be inspected using Android Studio's Database Inspector.

---

## 📚 Learning Outcome

After completing this practical, the student understands how to:

- Work with JSON data.
- Parse JSON responses.
- Communicate with an Internet API.
- Use `HttpURLConnection`.
- Display dynamic data with RecyclerView.
- Create and manage an SQLite database.
- Insert, query and delete database records.
- Use a `Cursor` to read SQLite data.
- Use `Serializable` with a model class.
- Connect network data, database storage and the Android UI.

---

## 👨‍💻 Project Information

**Practical:** 7  
**Project:** 24012011009_MAD_Practical-7  
**Platform:** Android  
**Language:** Kotlin  
**UI:** XML  
**Database:** SQLite

---

## 📌 Practical Summary

This practical connects three major parts of Android development:

```text
Internet API
     +
JSON Parsing
     +
SQLite Database
     +
RecyclerView
     ↓
Complete Android Application
```

The final application demonstrates retrieving structured data from the Internet, storing it locally, and presenting it through a RecyclerView-based user interface.
