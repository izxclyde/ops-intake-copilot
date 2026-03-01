# 🐛 [High] App crashes when uploading profile photo on iPhone Safari

## Description
The mobile app crashes immediately when attempting to upload a profile photo from the account settings screen.

## Environment
- **Device:** iPhone 14 Pro
- **OS:** iOS 17.5
- **Browser/App Context:** Safari (PWA mode)
- **App Version:** 1.12.0

## Steps to Reproduce
1. Open the app and sign in.
2. Navigate to **Profile**.
3. Tap **Upload Photo**.
4. Select an image from camera roll.
5. Tap **Confirm**.

## Expected Result
Profile photo uploads successfully and a success message appears.

## Actual Result
The app closes instantly after tapping **Confirm** and returns to iOS home screen.

## Severity
**High** — blocks account customization for all iOS Safari users.

## Original Report (Discord)
> App crashes when I try to upload a profile picture. Using iPhone 14 Pro with Safari. Click upload button, app closes immediately. This is critical.

## Metadata
- **Source:** Discord (`#bug-reports`)
- **Reported by:** `@jane_doe`
- **Message ID:** `1258392019384729102`
- **Intake Classification:** `complete_bug_report`
- **AI Model:** `Groq LLaMA 3`
- **Created by:** `Ops Intake Copilot`
