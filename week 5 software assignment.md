Technical Writing Lab
Name: Saferio Leirum Reshima
Course: Technical Writing
Date: 7 October 2026

Exercise A: User Manual Procedure
Creating a New Flutter Project and Running It on a Device
Prerequisites
Before starting, make sure you have:
•	A computer running Windows, macOS, or Linux.
•	The Flutter SDK installed on the computer.
•	Flutter added to the system PATH.
•	Visual Studio Code installed.
•	A web browser such as Google Chrome, or an Android emulator/physical device.
•	An internet connection for downloading Flutter packages.
•	Basic knowledge of opening and using a terminal.
Procedure
1. Open Visual Studio Code.
Expected result: Visual Studio Code opens and displays the main editor window.
2. Open the integrated terminal in Visual Studio Code.
Expected result: A terminal panel appears at the bottom of the Visual Studio Code window.
3. Navigate to the folder where you want to create the Flutter project.
Expected result: The terminal shows that you are inside the selected project folder.
4. Run the command flutter create my_first_app.
Expected result: Flutter creates a new project named my_first_app and generates the required project files.
5. Open the my_first_app folder in Visual Studio Code.
Expected result: The Flutter project files appear in the Explorer panel.
6. Run the command flutter devices.
Expected result: Flutter displays the devices available for running the application, such as Chrome, Windows, or an Android device.
7. Select an available device.
Expected result: The selected device becomes the target device for running the Flutter application.
8. Run the command flutter run.
Expected result: Flutter builds the application and launches it on the selected device.
9. Confirm that the Flutter application appears on the selected device.
Expected result: The default Flutter application appears on the selected device and displays the counter interface.
Screenshot Description
A screenshot should show Visual Studio Code with the my_first_app project open in the Explorer panel. The terminal should show that the Flutter application has been successfully launched, while the selected device or browser should display the default Flutter counter application.
Troubleshooting
Common problem: flutter is not recognized as a command.
This error usually occurs when the Flutter SDK has not been added to the system PATH.
Solution: Confirm that Flutter is installed and add the Flutter SDK's bin directory to the system PATH. After updating the PATH, restart Visual Studio Code and run:
flutter doctor

If Flutter is configured correctly, the command displays information about the Flutter installation and identifies any remaining configuration issues.
Exercise B: API Reference Entry
Create a Task
HTTP Method: POST
Endpoint: /api/v1/projects/{projectId}/tasks
Description
This endpoint allows an authenticated user to create a new task within a specific project. The task includes a title, an optional description, an assignee, a due date, and a priority level.
Path Parameters
Parameter	Data Type	Required	Description
projectId	String	Yes	The unique ID of the project where the new task will be created.
Example:
/api/v1/projects/proj-1024/tasks

In this example, proj-1024 is the project ID.
Request Body Parameters
The request body must be sent in JSON format.
Parameter	Data Type	Required	Description
title	String	Yes	The name or short title of the task.
description	String	No	Additional information about the task.
assigneeId	String	Yes	The unique ID of the user assigned to the task.
dueDate	String (ISO 8601 date)	Yes	The date by which the task should be completed.
priority	String	Yes	The priority of the task. Accepted values are low, medium, or high.
Request Headers
The following headers are required when sending a request to the endpoint:
Header	Required	Description
Authorization	Yes	Contains the user's access token used to authenticate the request.
Content-Type	Yes	Specifies that the request body is formatted as JSON.
Authentication
The API uses Bearer Token authentication. The access token must be included in the Authorization header.
Example:
Authorization: Bearer <access_token>
Content-Type: application/json

A valid access token is required to create a task.
Example Request
HTTP Request:
POST /api/v1/projects/proj-1024/tasks HTTP/1.1
Host: api.example.com
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
Content-Type: application/json

Request Body:
{
  "title": "Complete database documentation",
  "description": "Prepare the technical documentation for the project database.",
  "assigneeId": "usr-2048",
  "dueDate": "2026-10-15",
  "priority": "high"
}

HTTP Response Codes
Status Code	Description
201 Created	The task was successfully created.
400 Bad Request	The request contains invalid or incorrectly formatted data.
401 Unauthorized	Authentication is missing or the access token is invalid or expired.
403 Forbidden	The authenticated user does not have permission to create a task in the specified project.
404 Not Found	The specified project or assignee cannot be found.
409 Conflict	The request conflicts with the current state of the project or task data.
422 Unprocessable Entity	The request format is valid, but one or more values fail validation, such as an invalid priority value.
500 Internal Server Error	An unexpected error occurs on the server while processing the request.
Successful Response
HTTP Status: 201 Created
The API returns the newly created task when the request is successful.
Response Body:
{
  "id": "task-7834",
  "projectId": "proj-1024",
  "title": "Complete database documentation",
  "description": "Prepare the technical documentation for the project database.",
  "assigneeId": "usr-2048",
  "dueDate": "2026-10-15",
  "priority": "high",
  "status": "pending",
  "createdBy": "usr-1001",
  "createdAt": "2026-10-07T11:42:15Z",
  "updatedAt": "2026-10-07T11:42:15Z"
}

Response Fields
Field	Data Type	Description
id	String	Unique ID automatically assigned to the new task.
projectId	String	ID of the project containing the task.
title	String	Title of the task.
description	String	Additional information about the task.
assigneeId	String	ID of the user assigned to the task.
dueDate	String	Date by which the task should be completed.
priority	String	Task priority: low, medium, or high.
status	String	Current status of the task.
createdBy	String	ID of the user who created the task.
createdAt	String	Date and time when the task was created.
updatedAt	String	Date and time when the task was last updated.

