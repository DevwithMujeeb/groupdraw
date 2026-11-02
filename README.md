# GroupDraw

A free, open source 3D website that randomly assigns students to groups with one leader per group.
Built with three.js and Firebase (free Spark plan, no card needed, no paid functions).

## Setup (about 15 minutes)

1. Go to https://console.firebase.google.com and create a project.
2. Add a Web app (the </> icon). Copy the config values into `firebase-config.js`.
3. Authentication > Sign in method > turn on **Google**.
4. Firestore Database > Create database (production mode, any region).
5. Firestore > Rules > paste the contents of `firestore.rules` > Publish.
6. Host the folder. Netlify drag and drop works, or GitHub Pages. It must be served over https, not opened as a file.
7. Authentication > Settings > Authorized domains > add your hosting domain (for example yoursite.netlify.app).
8. Open the site, sign in with the admin email, set the class size, and press **Open the draw**.

## How the draw stays fair

- When you open the draw, all slots are shuffled once (for 52 students: groups 1 and 10 get 6, the rest get 5, with one random leader slot per group).
- A student's button only takes the next slot in that list. The database rules reject any attempt to pick a slot, redo a draw, or claim twice.
- Only school emails ending in @stu.ui.edu.ng with a verified address pass the rules, so the check cannot be bypassed from the browser.
- Matric numbers are unique.
- The admin browser generates the shuffle, so the admin could technically read it in the Firebase console. Press **Close and publish results** after the draw so the whole class can check group sizes and leaders.

## Admin

Sign in with the admin email to see the dashboard: live roster, CSV download, quote editor (changes appear for everyone), WhatsApp links per group, close and reset buttons.
Students only see the link for their own group, but any signed in student could read all links through the console, so treat the invite links as class only.

## If sign in fails for students

Google sign in only works if the school email is a Google account (for example Google Workspace). If UI student emails use Microsoft 365 instead, switch the provider in `index.html` to `OAuthProvider("microsoft.com")` and enable Microsoft in Firebase.
