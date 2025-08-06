# Full Stack Twitch Clone using Clerk, Supabase, and Stream Video + Chat

This repository demonstrates how to build a full-stack clone of Twitch, using the following tech:

- Web Framework: [Next.js](https://nextjs.org)
- Authentication: [Clerk](https://clerk.com)
- Database Storage: [Supabase](https://supabase.com)
- Livestreaming: [Stream Video](https://getstream.io/video/)
- Chat: [Stream Chat](https://getstream.io/chat/)

This repository is intended to be an accompanying piece for the tutorials we've created:

- [Video Tutorial on Youtube](https://youtu.be/xdaCukiHXzg) (comprehensive step-by-step guide, ~5h long)
- Blog posts (split up into digestible sections)
  - Part 1: [Project Description And Setup](https://getstream.io/blog/twitch-clone-project-setup)
  - Part 2: Authentication with Clerk (Coming Soon)
  - Part 3: Supabase User Integration
  - Part 4: Home Feed with Livestreaming Data
  - Part 5: Livestreams With Stream Video
  - Part 6: Adding and Customizing Stream Chat

If you enjoy this content, feel free to give this repo a ⭐️ and let us know what to build next on [X](https://x.com/getstream_io) or [LinkedIn](https://www.linkedin.com/company/getstream).

## How to run the project locally?

First of all, you should clone the repo with the following command:

```bash
git clone git@github.com:GetStream/twitch-clone-nextjs.git
```

Before running the project, you need to have accounts and projects setup for the following (if you're unsure about the setup process, it's well documented in [the video tutorial](https://youtu.be/xdaCukiHXzg)):

- [Clerk](https://clerk.com)
- [Supabase](https://supabase.com)
- [Stream](https://dashboard.getstream.io/)

Then, you need to create a local `.env` file in the root of your project and fill out the following values:

```
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=

NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=

STREAM_API_KEY=
NEXT_PUBLIC_STREAM_API_KEY=
STREAM_SECRET=


NEXT_PUBLIC_CLERK_SIGN_UP_FORCE_REDIRECT_URL=/createStreamUser
```

You can then first install all dependencies by running:

```bash
npm run build
```

And finally, run the project with:

```bash
npm run dev
```

This should host the project on `localhost:3000` (or another port if that one is occupied - check the console log in that case).

## Where can I learn more?

There are plenty of options to explore more about each tech involved. Feel free to go to each vendor's site and explore more.

If you're interested in Stream-related content in that realm, I recommend looking at the following links:

- [Stream Livestreaming Tutorial](https://getstream.io/video/sdk/react/tutorial/livestreaming/)
- [Stream's React SDK](https://getstream.io/video/docs/react/)
- [Backend SDKs documentation](https://getstream.io/chat/docs/node/)
- [Chat Tutorial](https://getstream.io/chat/react-chat/tutorial/)
- [Chat SDK](https://getstream.io/chat/docs/sdk/react/)

If you have requests, enjoyed the projects, or have any other questions, feel free to always contact us on [X](https://x.com/getstream_io) or [LinkedIn](https://www.linkedin.com/company/getstream). We hope you find value in this project and wish you the best for your endeavours!
