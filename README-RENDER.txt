RENDER DEPLOYMENT

1. Upload this ZIP's contents to a GitHub repository (files must be in the repository root).
2. In Render, choose New + -> Web Service and connect that repository.
3. Runtime: Python.
4. Build command: pip install -r requirements.txt
5. Start command: gunicorn app:app --bind 0.0.0.0:$PORT --workers 1 --threads 4 --timeout 120
6. Deploy.

IMPORTANT LIMITATIONS
- Render Free web services can spin down after inactivity. The in-app ping thread does not guarantee that Render will stay awake.
- The app stores data.json and uploaded server files on the local filesystem. On Render's free service, local files are ephemeral and may be lost on redeploy/restart. A persistent disk requires a paid plan and must be configured separately.
- This is a Flask web app, not a full VPS. Processes launched inside the panel are not guaranteed to remain running, get public ports, or survive deploys/restarts on Render. Use a VPS for reliable hosting of users' bots/servers.
- Change the default NORMAL_PASSWORD (currently 2015) by setting a secure NORMAL_PASSWORD environment variable in Render before exposing the site publicly.
