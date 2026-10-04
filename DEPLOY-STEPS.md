# Putting the SGH app v7.8 on Railway (4 October 2026)

These steps put v7.8 up as **a new GitHub repository and a new Railway service, with its own address**. Nothing here opens, changes or replaces v7.7: its repository, its Railway service and its address stay exactly as they are, so v7.7 is there all the time.

You need: the bundle `sgh-v7_8-deploy-04oct.zip`, a browser, and your GitHub and Railway sign-ins. About 20 minutes.

**What is new in this bundle (4 October, afternoon).** The app is now compiled, so it opens quickly on a phone, and the page shows a loading screen ("Southampton General Hospital", "Find My Way", "This takes a moment.") until the app appears. Babel, React and ReactDOM are no longer separate files: React and ReactDOM are built into the compiled app, and Babel is not needed. The preview route with pictures (Main Entrance to Eye Reception B) brings a `maps/ob8` folder of 11 pictures.

## What is in the bundle, and where each file goes

| In the bundle | Where it goes in the new repository | What it is |
|---|---|---|
| `server.js` | top level (not in a folder) | the web server Railway runs; it serves the `public` folder and nothing else |
| `package.json` | top level | tells Railway this is a Node app and to start it with `node server.js` |
| `railway.json` | top level | tells Railway how to start it and to check that it answers |
| `public/index.html` | `public` folder | the page, with the loading screen; it loads the compiled app |
| `public/sgh-v7_8-app.min.js` | `public` folder | the v7.8 app, compiled, with React and ReactDOM 18.3.1 built in |
| `public/routes/` (36 files, `sgh-routes-CB33.json` to `sgh-routes-WB38.json`) | `public/routes` folder | the directions: one file for each start |
| `public/maps/ob8/` (11 files, `map-01.png` to `map-14.png`) | `public/maps/ob8` folder | the pictures for the preview route, Main Entrance to Eye Reception B |
| `DEPLOY-STEPS.md` | not needed | these steps (harmless if you upload it) |

52 files go up in all: 3 at the top, 2 in `public`, 36 in `public/routes`, 11 in `public/maps/ob8`. The earlier bundle's `sgh-v7_8-app.js`, `react.production.min.js`, `react-dom.production.min.js` and `babel.min.js` are not in this bundle and are not needed.

## Part A: unzip, and make the new repository

1. Unzip `sgh-v7_8-deploy-04oct.zip` (right click, Extract All). You get a folder holding `server.js`, `package.json`, `railway.json`, `DEPLOY-STEPS.md` and a `public` folder.
2. Go to github.com and sign in. Click **+** (top right), then **New repository**.
3. Repository name: `sgh-wayfinding-v7-8` (any name that is not v7.7's repository). Private is fine. Tick **Add a README file**. Click **Create repository**.

## Part B: upload the files, in this order

4. In the new repository, click **Add file**, then **Upload files**.
5. From the unzipped folder, drag `server.js`, `package.json` and `railway.json` onto the page. Wait until all three are listed. Under "Commit changes", type `v7.8 server files`, then click **Commit changes**.
6. Click **Add file**, then **Create new file**. In the file name box, type `public/` (GitHub turns it into a folder), then `routes/` (a second folder), then `keep.txt`. The box now reads `public / routes / keep.txt`. In the large box below, type `Route files for v7.8.` Click **Commit changes...**, then **Commit changes**. This makes both folders.
7. On the repository's front page, click **Add file**, then **Create new file** again. In the file name box, type `public/`, then `maps/`, then `ob8/`, then `keep.txt`. The box now reads `public / maps / ob8 / keep.txt`. In the large box, type `Pictures for the preview route.` Click **Commit changes...**, then **Commit changes**.
8. Go back to the repository's front page (click the repository name at the top), click the **public** folder, then **Add file**, then **Upload files**. Drag these two files from the unzipped `public` folder: `index.html` and `sgh-v7_8-app.min.js`. Wait until both are listed. Type `v7.8 page and app`, then click **Commit changes**.
9. In the **public** folder, click the **routes** folder, then **Add file**, then **Upload files**. Open the unzipped `public\routes` folder, select all 36 files (Ctrl+A) and drag them onto the page. Wait until all 36 are listed. Type `v7.8 route files`, then click **Commit changes**.
10. In the **public** folder, click **maps**, then **ob8**, then **Add file**, then **Upload files**. Open the unzipped `public\maps\ob8` folder, select all 11 pictures (Ctrl+A) and drag them onto the page. Wait until all 11 are listed. Type `v7.8 preview pictures`, then click **Commit changes**.

   *A quicker way, if your browser allows it:* in step 5, drag the `public` folder as well as the three files. GitHub keeps the folders. Then skip steps 6 to 10 and do the check in step 11.

11. Check the repository: the front page shows the `public` folder, `README.md`, `package.json`, `railway.json` and `server.js`. `public` shows the `maps` and `routes` folders and the two files. `public/routes` shows the 36 route files, and `public/maps/ob8` the 11 pictures (each with `keep.txt` if you made it; leave them, they do no harm). Nothing else is needed.

## Part C: Railway, a new service with its own address

12. Go to railway.com and sign in. On the dashboard, do not open v7.7's project. Click **New** (or **+ New Project**), then **Deploy from GitHub repo**.
13. If `sgh-wayfinding-v7-8` is not in the list, click **Configure GitHub App**, give Railway access to `sgh-wayfinding-v7-8`, and come back.
14. Click `sgh-wayfinding-v7-8`. If Railway offers **Deploy Now**, click it. No variables are needed.
15. Railway builds and starts the app (a minute or two). In the new service, open **Deployments**: wait until the newest one shows as successful (Active). Click **View logs**: the deploy log ends with a line like `SGH wayfinding v7.8 listening on 0.0.0.0:8080 (51 files)` (49 if you made no `keep.txt` files).
16. Open the service's **Settings**, then **Networking**, then **Public Networking**, and click **Generate Domain**. If it asks for a port, type the number at the end of `0.0.0.0:` in the log line (usually 8080). Railway gives the new address, ending `.up.railway.app`. This is the v7.8 address; v7.7 keeps its own.
17. Open the new address on your phone. You may see the blue loading screen for a moment, then Find My Way with "You are here: Main Entrance".

## Part D: a two-minute check before giving UHS the address

18. Tap **Where I want to go**, then **Radiotherapy**, then **Start directions**: the first step shows.
19. Go back, choose **Eye Reception B**, and tap **See this route on maps (preview)**: the Route preview shows step 1 with its picture. Tap **Next step** a few times.
20. Open the address with `?tag=NWC94` on the end: You are here shows North Wing.
21. With the volume up, tap **Read this step aloud**: the step is read.

## If something goes wrong

- **On the day, if v7.8 misbehaves:** give UHS the v7.7 address instead. These steps never touched v7.7, so it is already there; nothing needs putting back.
- **To take v7.8 offline:** in Railway, open the v7.8 service, then **Settings**, **Networking**, and remove the generated domain. The address stops working; v7.7 is not affected. (Deleting the whole v7.8 service, at the foot of its Settings, also leaves v7.7 and both GitHub repositories as they are.)
- **If a later upload breaks v7.8:** in Railway, open the v7.8 service, then **Deployments**. On the last deployment that worked, open the three dots menu and choose **Rollback** (on some screens, **Redeploy**). That deployment comes back at once.
- **If v7.8 files were uploaded to v7.7's repository by mistake:** in Railway, open v7.7's service, then **Deployments**. On the last v7.7 deployment from before the mistake, open the three dots menu and choose **Rollback** (or **Redeploy**). The live v7.7 is back at once. Then, in v7.7's repository on GitHub, delete the files added by mistake (open each file, three dots menu, **Delete file**), so that the next v7.7 build is right again.

## Starting points: the `?tag=` addresses

There are no RouteLoop devices for the review, so a start is chosen in one of two ways:

- **On the app:** tap **Change** under "You are here" and choose any of the 36 places. Then **Where I want to go** lists all 21 destinations. UHS can choose any start and any destination on their own phones this way.
- **By the address:** put `?tag=` and the start's code on the end of the v7.8 address, as in the table. For example, if Railway gives `https://sgh-wayfinding-v7-8.up.railway.app`, the Oncology street entrance is `https://sgh-wayfinding-v7-8.up.railway.app/?tag=RA67A`. Capitals or small letters both work.

What the app shows:

- **With no tag:** the landing screen with "You are here: Main Entrance, Level C, Centre Block" and **Change** under it (a screen reader hears "Change where you are"). One exception: on the same phone, within 30 minutes of a journey, the address with no tag goes back to that journey. An address with a tag always starts fresh at that start.
- **With a tag the app does not know** (for example `?tag=ZZ999`): the same as no tag, Main Entrance with **Change**, and no message.
- **v7.7's six tag names still work:** `main-entrance-c` (Main Entrance), `pharmacy-c` (Outpatient Pharmacy), `lift-ww` (West Wing lift lobby, Level C), `lift-ew` (East Wing lift lobby, Level C), `eaterie-b` (Paddy and Scott's and Feast), `macmillan-b` (The Patient and Family Support Hub).

The 36 starts, in the order of the You are here list:

| # | Start name | Shown under it | In the list under | Code | Address ending |
|---|---|---|---|---|---|
| 1 | Main Entrance | Level C, Centre Block | Entrances | CC380 | `/?tag=CC380` |
| 2 | North Wing | Level C, North Wing | Entrances | NWC94 | `/?tag=NWC94` |
| 3 | West Wing | Level B, West Wing | Entrances | WB38 | `/?tag=WB38` |
| 4 | Wessex Neurological Centre | Level B, Neurology Centre | Entrances | NB100 | `/?tag=NB100` |
| 5 | Eye Unit | Level B, Eye Unit | Entrances | OB03 | `/?tag=OB03` |
| 6 | Eye Emergency | Level B, Eye Unit | Entrances | OB01 | `/?tag=OB01` |
| 7 | Wessex Neurological Centre | Level A, Neurology Centre | Entrances | NA001 | `/?tag=NA001` |
| 8 | Neuro Outpatients | Level A, Neurology Centre | Entrances | NA002 | `/?tag=NA002` |
| 9 | Radiotherapy | Level A, Oncology Centre | Entrances | RA01 | `/?tag=RA01` |
| 10 | Oncology street entrance | Level A, Oncology Centre | Entrances | RA67A | `/?tag=RA67A` |
| 11 | South Academic Block and Lab and Pathology | Level A, Lab and Pathology | Entrances | LA74 | `/?tag=LA74` |
| 12 | Main reception desk | Level C, Centre Block | Level C | CC386 | `/?tag=CC386` |
| 13 | Shops and M&S Cafe | Level C, Centre Block | Level C | CC390 | `/?tag=CC390` |
| 14 | Outpatient Pharmacy | Level C, Centre Block | Level C | CC44 | `/?tag=CC44` |
| 15 | Children's Outpatients | Level C, Centre Block | Level C | CC210 | `/?tag=CC210` |
| 16 | CT Main | Level C, Centre Block | Level C | CC81 | `/?tag=CC81` |
| 17 | MRI | Level C, Centre Block | Level C | CC577B | `/?tag=CC577B` |
| 18 | Oral and Maxillofacial Unit (maxfax) | Level C, Centre Block | Level C | CC166 | `/?tag=CC166` |
| 19 | Inpatient Pharmacy | Level C, Centre Block | Level C | CC28A | `/?tag=CC28A` |
| 20 | Blood Tests (adults) | Level C, Lab and Pathology | Level C | LC1 | `/?tag=LC1` |
| 21 | East Wing lift lobby | Level C, East Wing | Level C | EC1 | `/?tag=EC1` |
| 22 | West Wing lift lobby | Level C, Centre Block | Level C | CC101B | `/?tag=CC101B` |
| 23 | Neuro lift lobby | Level C, Neurology Centre | Level C | NC006 | `/?tag=NC006` |
| 24 | Oncology Reception | Level B, Oncology Centre | Level B | RB56 | `/?tag=RB56` |
| 25 | Therapies | Level B, West Wing | Level B | WB28 | `/?tag=WB28` |
| 26 | Paddy and Scott's and Feast | Level B, Centre Block | Level B | CB42 | `/?tag=CB42` |
| 27 | The Patient and Family Support Hub | Level B, East Wing | Level B | EB112 | `/?tag=EB112` |
| 28 | Eye Emergency reception | Level B, East Wing | Level B | EB169 | `/?tag=EB169` |
| 29 | Eye Reception B | Level B, Eye Unit | Level B | OB8 | `/?tag=OB8` |
| 30 | Eye Reception A | Level B, Oncology Centre | Level B | RB113B | `/?tag=RB113B` |
| 31 | Cross Sectional Imaging MRI and CT | Level B, Neurology Centre | Level B | NB206 | `/?tag=NB206` |
| 32 | West Wing lift lobby | Level B, Centre Block | Level B | CB33 | `/?tag=CB33` |
| 33 | East Wing lift lobby | Level B, East Wing | Level B | EB1 | `/?tag=EB1` |
| 34 | Radiotherapy | Level A, Oncology Centre | Level A | RA24 | `/?tag=RA24` |
| 35 | Neurological Outpatients | Level A, Neurology Centre | Level A | NA112 | `/?tag=NA112` |
| 36 | Oncology lift lobby | Level A, Oncology Centre | Level A | RA75 | `/?tag=RA75` |

## Remaking the compiled app after a change

The JSX, `Southampton_General_Hospital_v7_8app.jsx`, is the source of record. `public/sgh-v7_8-app.min.js` is made from it, and must be remade after any change to it. This is a job for the app build, not for the upload:

- **Tool:** esbuild 0.24.2, with React 18.3.1 and ReactDOM 18.3.1, on Node 20 or later. In the folder holding the JSX: `npm install --no-save esbuild@0.24.2 react@18.3.1 react-dom@18.3.1`
- **Entry file**, `deploy_build/entry.jsx`, four lines:

  ```
  import React from 'react';
  import { createRoot } from 'react-dom/client';
  import App from '../Southampton_General_Hospital_v7_8app.jsx';
  createRoot(document.getElementById('root')).render(<App />);
  ```

- **Command**, from the folder holding the JSX (also in `deploy_build/build_app.sh`):

  ```
  npx esbuild deploy_build/entry.jsx --bundle --minify --format=iife --jsx=automatic --loader:.jsx=jsx --define:process.env.NODE_ENV='"production"' --outfile=deploy_04oct/public/sgh-v7_8-app.min.js
  ```

- The same command builds the preview page's app (`preview/build_preview.sh`), so the preview file and the deployed app run the same compiled code.
- If the route files or the pictures change, they are remade by `make_v7_8.py` (with `--route-files routes` and `--maps data/maps/ob8/maps.json`) and copied into `public/routes` and `public/maps/ob8`.

## Good to know

- The app is compiled (your decision of 4 October), with React and ReactDOM built in, so it needs no Babel and no other website, except Google Fonts for the Nunito lettering. If that does not load, the phone's own lettering is used and everything still works.
- The loading screen shows as soon as the page itself arrives, before the app does, and goes when the app appears. A first visit downloads about 83 KB.
- These timings were measured on a slowed connection with a slowed processor:

  | Connection | To the landing screen | Before (zero-build) |
  |---|---|---|
  | Good Wi-Fi | about 0.3 seconds | 2.4 |
  | Slow 4G | about 1.8 seconds | 6.8 |
  | 3G | about 5.7 seconds | 18.8 |

- The preview pictures are fetched only when the Route preview is opened, one picture as each step shows (about 20 to 40 KB each). Nothing else in the app fetches them.
- The server writes no record of visitors. Feedback and the Yes, OK, No answers are not sent anywhere.
- To try the bundle on a computer first (optional): with Node 20 or later installed, open a terminal in the unzipped folder, run `node server.js`, and open `http://localhost:3000/` in a browser.
