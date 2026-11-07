# vidgrab-keepalive

Render's free plan stops a web service after 15 minutes without traffic. This
repository sends a request to `/api/health` every 5 minutes so the service
never spins down.

Public on purpose: GitHub Actions minutes are unlimited for public
repositories, so the pings cost nothing.

## Setup

1. Open **Settings → Secrets and variables → Actions → Variables**.
2. **New repository variable**
   - Name: `VIDGRAB_URL`
   - Value: `https://your-service.onrender.com`
3. Open the **Actions** tab → **keepalive** → **Run workflow** to test it once.

The schedule starts on its own within a few minutes.

## Notes

- GitHub's scheduler can drift a few minutes under load. Five-minute spacing
  leaves room before the 15-minute sleep timer.
- GitHub pauses scheduled workflows after 60 days without repository activity.
  Open the Actions tab and click **Run workflow** once every couple of months,
  or push any commit.
- Render's free plan allows 750 instance-hours per month. Always-on is about
  730, so keep this to one service.
- The workflow fails loudly if `VIDGRAB_URL` is missing.
