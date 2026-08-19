# Calmora QuickSend

**Calmora QuickSend** is a privacy-first file-sharing utility designed to make sending files simple, fast, and comfortable. It combines a clean Calmora-inspired interface with practical file-sharing tools, allowing users to upload files, create shareable links, optionally protect those links with a password, choose how long the share remains available, and send the link by email.

QuickSend is designed as a separate utility within the Calmora ecosystem. While it uses Calmora's calm visual language, it has its own purpose, interface, and identity. The goal is straightforward: **select your files, create a share, send it, and let it expire automatically when you no longer need it.**

---

## ✨ Features

### 📁 Simple File Uploading

QuickSend provides a straightforward upload experience designed for both desktop and mobile devices.

Users can:

* Select files from their device.
* Select multiple files at once.
* Drag and drop files where supported.
* See upload progress.
* Receive clear feedback when something goes wrong.
* Review the files selected before creating a share.
* Remove files before uploading.
* Create a share containing multiple files.

The interface is designed to avoid unnecessary steps. QuickSend focuses on getting from a file on your device to a usable share link as quickly as possible.

---

## 🔗 Expiring Share Links

After files are uploaded, QuickSend creates a share link that can be given to another person.

Share expiration can be configured using preset durations:

* **1 hour**
* **24 hours**
* **7 days**
* **30 days**

Expiration is an important part of QuickSend's design. Files do not need to remain available indefinitely when they were only intended for a temporary transfer.

Once a share expires, it is treated as unavailable and can be cleaned up by the backend.

This makes QuickSend useful for temporary transfers, documents, media, project files, personal files, and other content that does not need permanent hosting.

---

## 🔐 Optional Password Protection

QuickSend can optionally protect a share with a password.

When password protection is enabled, the recipient must provide the correct password before accessing the protected share.

This provides an additional layer of protection for links that may contain information the sender does not want to make openly accessible to anyone who happens to receive the URL.

Password protection is optional so that users can choose between convenience and an additional access-control step depending on what they are sharing.

---

## 📤 Sharing Tools

Once a share has been created, QuickSend provides several ways to distribute it.

### Copy Link

The generated URL can be copied directly to the clipboard.

This makes it easy to paste the link into:

* Messages
* Discord
* Social platforms
* Documents
* Notes
* Other websites
* Email
* Any application that accepts text

### Native Share

On supported devices and browsers, QuickSend can use the device's native sharing functionality.

This can make sharing especially convenient on mobile devices.

### Email

QuickSend also provides an email sending form so that users can send the generated share link directly to a recipient.

The backend handles email delivery through Google Apps Script.

---

# 📦 My Shares

QuickSend includes a **My Shares** area for viewing shares created by the user.

The area is designed to provide an overview of:

* Active shares
* Expired shares
* Share information
* Expiration information
* Available management actions

Users can also revoke or delete shares where supported.

The purpose of My Shares is to give users a central place to keep track of temporary files instead of requiring them to remember every link they have created.

---

# 🗑️ Revoking Shares

A share does not necessarily need to remain active until its scheduled expiration time.

QuickSend provides revoke/delete functionality so that a user can remove access to a share earlier when it is no longer needed.

For example, a user might create a share that lasts for 30 days but decide after two days that the recipient no longer needs access.

Instead of waiting for the 30-day expiration, the share can be revoked.

---

# ⏳ Automatic Expiration

Automatic expiration is one of the core ideas behind QuickSend.

When a share reaches its configured expiration time, it should no longer be considered active.

The backend can use expiration metadata to determine whether a share is still valid.

Expired shares can then be cleaned up as part of backend maintenance.

This reduces unnecessary long-term storage and keeps temporary transfers temporary.

---

# 🔒 Privacy-First Design

QuickSend is designed around the idea that file sharing should not require creating a permanent account simply to send a file.

The project emphasizes:

* No account required for basic sharing.
* Temporary share links.
* Configurable expiration.
* Optional password protection.
* Automatic expiration.
* Encryption in transit through HTTPS.
* Clear privacy messaging.
* Minimal unnecessary information collection.

The goal is not to create another social network or permanent cloud-storage platform.

QuickSend is a utility.

Upload what you need, share it, and let the temporary share disappear when it is no longer needed.

---

# 🛡️ Security Philosophy

QuickSend uses several layers of protection rather than relying on one feature.

## HTTPS

When deployed over HTTPS, communication between the browser and the server is encrypted in transit.

This helps protect information while it travels between the user's device and the service.

## Expiration

Temporary links reduce the amount of time a file remains available.

## Password Protection

Optional passwords provide another access-control mechanism for protected shares.

## Backend Validation

The backend should validate incoming requests rather than trusting values supplied directly by the browser.

This includes checking expected request structures, file metadata, share identifiers, expiration information, and other relevant values.

## Controlled Storage

Uploaded files are stored using Google Drive through the Google Apps Script backend rather than being embedded directly inside the web page.

---

# ☁️ Backend Architecture

QuickSend uses a Google Apps Script + Google Drive architecture.

The frontend is responsible for the user experience.

The backend handles operations that should not be performed purely inside the browser.

The general architecture is:

```text
User Device
    │
    ▼
QuickSend Frontend
    │
    │ HTTPS requests
    ▼
Google Apps Script
    │
    ├── Google Drive
    │      └── Uploaded files
    │
    └── Email service
           └── Share notifications
```

This separation allows the frontend to remain lightweight while Google Apps Script handles server-side operations.

---

# 🗂️ Google Drive Storage

Google Drive acts as the storage layer for uploaded files.

When a user creates a share, the backend can store the uploaded content in the configured Drive location and associate it with metadata describing the share.

Metadata may include information such as:

* Share identifier
* File identifier
* File name
* File type
* File size
* Creation time
* Expiration time
* Password-protection status
* Share status

The exact implementation depends on the backend configuration used by the deployment.

Google Drive provides the underlying storage while Google Apps Script provides the application logic around that storage.

---

# 📧 Email Sending

QuickSend can send share links through the backend.

The frontend submits the required information to Google Apps Script, and the backend creates the email.

This avoids requiring users to configure an email provider inside the browser.

A typical flow is:

```text
Create Share
     │
     ▼
Receive Share URL
     │
     ▼
Enter Recipient Email
     │
     ▼
Frontend sends request
     │
     ▼
Google Apps Script
     │
     ▼
Email sent to recipient
```

The recipient receives the share information and can use the provided link to access the files while the share remains active.

---

# 🧹 Cleanup

Temporary files should not remain stored forever simply because they were once uploaded.

QuickSend's backend architecture supports expiration cleanup.

A cleanup process can identify shares whose expiration time has passed and remove or disable the associated content.

This can help keep the storage system organized and reduce unnecessary accumulation of expired files.

Cleanup behavior depends on the Google Apps Script deployment and configured triggers.

---

# 🖥️ Responsive Interface

QuickSend is designed to work across different screen sizes.

The interface should adapt to:

* Desktop computers
* Laptops
* Tablets
* Mobile phones

The layout uses responsive cards, flexible containers, accessible controls, and touch-friendly interactions.

The goal is to keep the same basic workflow regardless of device:

**Choose files → Configure share → Upload → Get link → Share**

---

# 🌿 Calmora Visual Identity

QuickSend uses visual elements inspired by Calmora while remaining a separate utility.

The design language includes:

* Mint and teal tones
* Rounded cards
* Soft shadows
* Subtle gradients
* Clean typography
* Spacious layouts
* Simple controls
* Gentle visual transitions
* Calm interface elements

The interface intentionally avoids an overly complicated enterprise-storage appearance.

QuickSend should feel approachable and lightweight.

The Calmora connection is visible through the visual language rather than making the product feel like the same page as another Calmora service.

---

# 🧭 Basic User Flow

A typical QuickSend session looks like this:

### 1. Open QuickSend

The user opens the QuickSend website.

### 2. Select Files

The user chooses one or more files.

### 3. Review Files

QuickSend displays the selected files so the user can confirm what will be shared.

### 4. Choose Expiration

The user chooses one of the available expiration presets.

### 5. Enable Password Protection

If needed, the user enables password protection and provides a password.

### 6. Upload

QuickSend sends the files to the backend.

### 7. Create Share

The backend creates the share information and returns the generated link.

### 8. Share

The user can copy the link, use native sharing, or send it through email.

### 9. Manage

The user can review the share through My Shares and revoke it when necessary.

### 10. Expiration

When the expiration time is reached, the share becomes unavailable and can be cleaned up.

---

# 📂 Project Structure

A typical QuickSend deployment may contain files similar to:

```text
Calmora-QuickSend/
│
├── index.html
├── style.css
├── script.js
├── README.md
│
└── assets/
    ├── images/
    ├── icons/
    └── other-assets/
```

The exact structure can vary depending on how the frontend was exported or built.

`index.html` is the main entry point for the website.

A separate CSS file can contain visual styling when the project is split into multiple files.

A JavaScript file can contain frontend behavior and communication with the backend.

`README.md` contains project documentation.

Assets can include logos, icons, illustrations, or other resources used by the interface.

---

# 🚀 Running the Frontend

Because the frontend is a web project, it can be hosted on a static website platform.

Examples include GitHub Pages and other static hosting services.

The important requirement is that the frontend can make requests to the configured backend endpoint.

If the project uses separate CSS, JavaScript, or asset files, those files must also be uploaded to the hosting environment while preserving the expected file paths.

---

# 🐙 GitHub Deployment

QuickSend can be stored in a GitHub repository.

A basic repository can contain:

```text
index.html
style.css
script.js
README.md
assets/
```

After uploading the project, GitHub Pages can be enabled from the repository settings.

A typical GitHub Pages configuration uses:

```text
Branch: main
Folder: / (root)
```

The website can then be accessed through the GitHub Pages address associated with the repository.

The README is not required for the website itself, but it provides useful documentation for anyone viewing the repository.

---

# ⚙️ Backend Setup

The backend uses Google Apps Script.

The general setup process is:

1. Create or open the Google Apps Script project.
2. Add the QuickSend backend code.
3. Configure the Google Drive storage location.
4. Configure the required backend settings.
5. Deploy the script as a web app.
6. Configure the deployment access settings required by the application.
7. Copy the deployed web-app endpoint.
8. Add the endpoint to the QuickSend frontend configuration.
9. Test uploading a file.
10. Test generating a share link.
11. Test opening the generated share.
12. Test expiration and deletion behavior.
13. Test email delivery if email sending is enabled.

The exact configuration values should remain in the backend or appropriate configuration area rather than being unnecessarily exposed in public frontend files.

---

# 🔧 Configuration

The frontend may need to know the URL of the deployed Google Apps Script web application.

That endpoint allows the browser to communicate with the backend.

A deployment may also require configuration for:

* Google Drive storage
* Email sending
* Expiration handling
* File validation
* Share metadata
* Cleanup triggers

Configuration should be reviewed whenever the backend deployment is changed.

If a new Apps Script deployment creates a different web-app URL, the frontend must be updated to use the new endpoint.

---

# 🧪 Testing Checklist

Before considering a deployment ready, test the complete workflow.

### Upload

* Select one file.
* Select multiple files.
* Test drag and drop where available.
* Test an unsupported file.
* Test an oversized file.
* Cancel/remove a selected file.

### Share Creation

* Create a 1-hour share.
* Create a 24-hour share.
* Create a 7-day share.
* Create a 30-day share.
* Create a password-protected share.
* Create a normal share without a password.

### Link

* Copy the generated link.
* Open it in another browser.
* Open it on another device.
* Confirm the files can be accessed while the share is active.

### Password

* Open a protected share.
* Enter the correct password.
* Test an incorrect password.
* Confirm protected content is not immediately exposed without the required password.

### Email

* Enter a valid recipient address.
* Send the share.
* Confirm the recipient receives the email.
* Open the link from the email.

### My Shares

* Confirm active shares appear.
* Confirm expired shares are represented correctly.
* Test revoke/delete functionality.

### Expiration

* Confirm expired shares are rejected.
* Confirm cleanup behavior works as expected.

---

# ⚠️ Error Handling

QuickSend should provide understandable errors instead of exposing technical backend information to users.

Possible errors include:

* No file selected
* Unsupported file
* File too large
* Upload failed
* Share creation failed
* Invalid share
* Share expired
* Incorrect password
* Invalid email address
* Email delivery failure
* Backend unavailable
* Network connection problem

A useful error should explain what happened and, where possible, what the user should do next.

---

# ♿ Accessibility

The interface should remain usable by as many people as possible.

Recommended accessibility practices include:

* Clear text labels
* Sufficient contrast
* Keyboard-accessible controls
* Visible focus states
* Descriptive buttons
* Meaningful error messages
* Responsive text sizing
* Avoiding interactions that depend entirely on hover
* Proper HTML structure
* Appropriate labels for form fields

Accessibility should be considered during future updates rather than added only at the end.

---

# 📱 Mobile Experience

QuickSend is intended to work on mobile devices as well as computers.

Mobile users should be able to:

* Select files from their device.
* Upload multiple files.
* Copy links.
* Use native sharing.
* Enter email addresses.
* Enter passwords.
* Review active shares.
* Manage shares.

Buttons and input controls should remain large enough to use comfortably on touchscreens.

---

# 🧩 Extensibility

QuickSend is structured so that additional functionality can be introduced later without changing its fundamental purpose.

Potential areas for future development include:

* More expiration presets
* Additional sharing controls
* Improved upload progress
* More detailed share information
* Improved file previews
* Additional management tools
* Better cleanup scheduling
* Expanded notification options
* More detailed storage management
* Additional accessibility improvements

Future features should preserve the core philosophy of QuickSend: simple temporary file sharing without unnecessary complexity.

---

# 🔏 Privacy Considerations

A file-sharing service handles potentially sensitive information, so privacy should remain a major consideration during development.

The application should avoid collecting information that is not necessary for its functionality.

Users should be clearly informed about how uploaded files are handled, how long they remain available, and what happens when a share expires.

The service should not imply that temporary sharing automatically makes a file completely private or impossible for others to access. Anyone who receives an active share link may potentially attempt to use it, and users should choose password protection when additional access control is appropriate.

The project should also keep backend credentials, secrets, and administrative configuration out of publicly accessible frontend files and repositories.

---

# 🔑 Secrets and Credentials

Do not commit private credentials to GitHub.

Examples of information that should not be publicly exposed include:

* API keys
* Passwords
* Private tokens
* Service credentials
* Private deployment information
* Administrative secrets

Public frontend code should contain only information that is safe to expose to website visitors.

Google Apps Script authorization and Google Drive access should be handled through the Google account and Apps Script environment rather than by placing private credentials inside `index.html`.

---

# 📜 License

This repository can be assigned a license appropriate for the project and its intended distribution.

If no license has been added, the source code should not automatically be assumed to be freely reusable simply because it is visible on GitHub.

Add a license file when the project owner has decided how the code may be copied, modified, or redistributed.

---

# 🌱 About Calmora

Calmora is the broader identity behind the project's visual language.

QuickSend extends that identity into a practical utility rather than a relaxation-focused experience.

The design intentionally keeps the recognizable Calmora-inspired softness while making the application feel purpose-built for file transfers.

The result is a utility that aims to feel clean, quiet, and straightforward instead of cluttered with unnecessary controls.

---

# 📌 Project Goals

The main goals of Calmora QuickSend are:

1. Make temporary file sharing easy.
2. Avoid requiring an account for basic sharing.
3. Support multiple files.
4. Provide useful expiration options.
5. Offer optional password protection.
6. Make generated links easy to distribute.
7. Provide email sharing.
8. Give users a place to manage their shares.
9. Automatically handle expired content.
10. Keep the interface responsive.
11. Use a privacy-conscious architecture.
12. Maintain a clean Calmora-inspired visual identity.
13. Keep the overall workflow understandable for everyday users.

---

# 🏗️ Technology

The project is built around standard web technologies and Google's cloud tooling.

### Frontend

* HTML
* CSS
* JavaScript

### Backend

* Google Apps Script

### Storage

* Google Drive

### Email

* Google Apps Script email functionality

### Hosting

The frontend can be deployed using a static web-hosting provider such as GitHub Pages.

This architecture keeps the frontend simple while giving the project a backend capable of handling storage, metadata, expiration, and email operations.

---

# 🔄 Data Flow

A simplified share creation flow looks like this:

```text
                 ┌──────────────────┐
                 │     User         │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ QuickSend Web UI │
                 └────────┬─────────┘
                          │
                    Upload Request
                          │
                          ▼
                 ┌──────────────────┐
                 │ Google Apps      │
                 │ Script Backend   │
                 └───────┬──────────┘
                         │
             ┌───────────┴───────────┐
             ▼                       ▼
     ┌────────────────┐     ┌────────────────┐
     │ Google Drive   │     │ Share Metadata │
     │ File Storage   │     │ / Expiration   │
     └────────────────┘     └────────────────┘
                         │
                         ▼
                  Generated Share
                         │
                         ▼
                  User receives URL
```

This architecture separates the user interface from the storage and server-side processing layer.

---

# 🛠️ Maintenance

When maintaining QuickSend, changes should be tested against the complete upload and sharing flow.

Backend changes should be tested for:

* Upload compatibility
* Existing shares
* Expiration logic
* Password protection
* File retrieval
* Deletion
* Email sending
* Error responses

Frontend changes should be tested on both desktop and mobile layouts.

When changing backend endpoints or deployment versions, verify that the frontend is still pointing to the correct deployed service.

---

# 📈 Performance

QuickSend should remain lightweight wherever practical.

The frontend should avoid loading unnecessary libraries or assets.

Images should be optimized where appropriate.

JavaScript should avoid unnecessary repeated requests.

Backend operations should return concise responses and avoid unnecessary processing.

Large files are inherently more demanding than small files, so upload progress and clear error handling are especially important for larger transfers.

---

# 🧠 Design Principle

QuickSend follows one simple idea:

> **Temporary files should be easy to send and easy to stop sharing.**

The application does not need to turn every file into a permanent cloud-storage object.

Instead, it focuses on the moment when a person needs to move a file from one place to another.

Choose the files.

Set the expiration.

Protect them if needed.

Create the link.

Send it.

When the share is no longer needed, revoke it or let it expire.

---

# 🚀 Quick Start

For a basic deployment:

```text
1. Upload the frontend files to your hosting provider.
2. Deploy the Google Apps Script backend.
3. Configure Google Drive storage.
4. Configure the backend endpoint in the frontend.
5. Open QuickSend.
6. Select a file.
7. Choose an expiration period.
8. Optionally enable password protection.
9. Upload the file.
10. Copy or share the generated link.
```

For GitHub Pages:

```text
Repository
   ↓
Upload project files
   ↓
Commit changes
   ↓
Settings
   ↓
Pages
   ↓
Deploy from main
   ↓
/ (root)
   ↓
Save
   ↓
QuickSend goes live
```

---

# 📄 Repository Contents

The repository should contain the files required to run and document the frontend.

A clean project may look like:

```text
/
├── index.html
├── style.css
├── script.js
├── README.md
└── assets/
```

The exact names may differ depending on the exported project.

The important rule is that every file referenced by the HTML or JavaScript must be present at the expected path.

If an image, stylesheet, JavaScript file, font, or other asset is referenced by the website but missing from the repository, parts of the application may fail to load correctly.

---

# 🔍 Troubleshooting

### The page loads but uploads fail

Check that the configured Google Apps Script web-app URL is correct and that the backend deployment is accessible.

### The generated link does not open

Check the share identifier, backend response, Drive file permissions, and expiration state.

### Email does not arrive

Check the recipient address, Apps Script email configuration, execution logs, and any applicable sending limits.

### The website looks unstyled

Check that the CSS file exists in the repository and that the path referenced by `index.html` is correct.

### JavaScript features do not work

Check that the JavaScript file exists, the script path is correct, and the browser console does not report errors.

### Images do not appear

Check that the image files were uploaded and that their paths match the references used by the frontend.

### A share says it has expired

Check the configured expiration timestamp and the backend's current time and expiration logic.

---

# 📜 Versioning

Future releases can use version numbers to make changes easier to track.

For example:

```text
v1.0.0
v1.1.0
v1.2.0
v2.0.0
```

Major versions can represent significant architectural or interface changes.

Minor versions can introduce new features.

Patch versions can contain bug fixes and small improvements.

---

# 💚 Calmora QuickSend

Calmora QuickSend is built around a simple combination:

**privacy-conscious sharing + temporary links + simple design.**

It is intended to be useful without feeling complicated.

Whether a user needs to send a few photos, a document, a collection of project files, or another temporary file bundle, QuickSend provides a straightforward workflow for getting those files from sender to recipient.

The Calmora-inspired interface keeps the experience visually calm, while the backend provides the functionality required for actual file sharing.

---

## Final Summary

Calmora QuickSend is a web-based temporary file-sharing utility with:

* 📁 Multi-file uploading
* 🖱️ Drag-and-drop support
* 📱 Responsive desktop and mobile design
* ⏱️ 1-hour, 24-hour, 7-day, and 30-day expiration
* 🔐 Optional password protection
* 🔗 Generated share links
* 📋 Copy-to-clipboard sharing
* 📤 Native device sharing
* 📧 Email sharing
* 🗂️ My Shares management
* 🗑️ Revoke/delete controls
* 🧹 Expiration cleanup
* ☁️ Google Drive storage
* ⚙️ Google Apps Script backend
* 🔒 HTTPS/encryption-in-transit support
* 🌿 Calmora-inspired visual design
* 🚫 No account required for basic sharing

The project is designed to make temporary file transfers feel simple rather than complicated.

**Calmora QuickSend — send it, share it, and let it expire.**
