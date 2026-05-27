# Deploying L3MON — Quick Start

Prerequisites:
- Java Runtime Environment 8 (JRE 1.8)
- Node.js and npm
- Git
- (Optional) `pm2` for background process management

1. Clone the repository:

```bash
git clone https://github.com/your-username/l3mon.git
cd l3mon
```

2. Install dependencies:

```bash
npm install
```

3. Configuration:
- Open `includes/const.js` and adjust `web_port`, `control_port`, and any path settings to match your environment. Default web port is `22533`.

4. Database (built-in file DB):
- L3MON uses `lowdb` and stores data in `maindb.json` and `clientData/*.json` in the repo root. The `maindb.json` file is created on first run.
- To set an admin username/password, stop the server and edit `maindb.json` under the `admin` object. The `password` field expects a lowercase MD5 hash.

5. Start L3MON:
- To run in the foreground:

```bash
node index.js
```

- Or using `npm start` (provided in `package.json`):

```bash
npm start
```

- To run in the background with `pm2`:

```bash
npm install -g pm2
pm2 start index.js --name l3mon
pm2 startup
pm2 save
```

6. Access the web interface:
- Open your browser to `http://localhost:22533` (or `http://<server-ip>:<web_port>` if running remotely).

7. Optional — APK builder requirements:
- Building payloads requires Java and the files in `app/factory/` (`apktool.jar`, `sign.jar`, and the `decompiled/` directory). Ensure Java 8 is available on the machine used for builds.

Troubleshooting tips:
- If `maindb.json` is not generated, verify write permissions in the repository root.
- If the web UI doesn't appear, confirm the `web_port` in `includes/const.js` and firewall rules.

For advanced configuration and troubleshooting, refer to the project's `README.md` and source files such as `includes/const.js` and `includes/databaseGateway.js`.
