# Personal S3 Static Site (Starter)

Auto-deploy to **Amazon S3** via **GitHub Actions**. Bucket used: `epamcloudproject`.

## How to use (super short)
1. **Unzip** this folder.
2. Open in **VS Code**.
3. Run:
   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin <your-new-empty-github-repo-url>
   git push -u origin main
   ```
4. In GitHub → **Settings → Secrets and variables → Actions**, add repository secrets:
   - `AWS_ACCESS_KEY_ID`
   - `AWS_SECRET_ACCESS_KEY`
   - `AWS_REGION` (e.g., `us-east-1`)
   - `S3_BUCKET_NAME` = `epamcloudproject`
5. In AWS S3:
   - Create bucket: **epamcloudproject** (uncheck *Block all public access*).
   - Properties → **Static website hosting** → Enable → Index: `index.html`, Error: `error.html`.
   - Permissions → **Bucket policy** → paste contents of `bucket-policy.json`.

After you push to **main**, GitHub Actions will sync this site to the S3 bucket.

## Files
- `.github/workflows/deploy.yml` – CI that deploys on push to `main`.
- `index.html`, `css/style.css`, `js/main.js`, `error.html` – static site files.
- `bucket-policy.json` – copy this into the S3 bucket policy (adjust if you ever change the bucket name).

## Notes
- If your bucket uses *Object Ownership = Bucket owner enforced* (ACLs disabled), the included policy is sufficient for public read. No `--acl public-read` needed.
- For HTTPS + custom domain, add **CloudFront + ACM + Route 53** later.
