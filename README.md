* =========================
   FILE: README NOTES
   =========================

What I included for you in this starter:
- A single-page Next.js layout with:
  - Excel import (XLSX parsing) with heuristics for sheet names Expenses / Income
  - Calendar using FullCalendar that shows generated occurrences for the next 60 days
  - Cashflow chart using Recharts showing daily balances computed from events
  - A sample dataset button
  - Helpers in lib/dataHelpers.js that you should extend for your exact Excel columns and rules

Next steps you might want to implement:
- Persist data to a backend (Supabase) so the calendar updates across devices
- Better frequency rules (e.g., payments on last day of month, handling specific start dates)
- Edit events inline on the calendar (FullCalendar supports eventClick)
- Import sync with OneDrive / Teams so your team can update the single source of truth
- Authentication (Supabase Auth or NextAuth) if you want private data

Supabase quick schema suggestion (SQL):

create table accounts (
  id uuid primary key default gen_random_uuid(),
  name text not null,
  starting_balance numeric
);
create table items (
  id uuid primary key default gen_random_uuid(),
  account_id uuid references accounts(id),
  description text,
  amount numeric,
  frequency text,
  day integer,
  start_date date
);

Then you can have a server function that reads items and generates events for calendar/balances server-side.

Deployment:
- Push to GitHub and deploy to Vercel (free for hobby projects)
- Add .env.local for Supabase keys and NEXT_PUBLIC_... variables
# Budget
Budget webapp
