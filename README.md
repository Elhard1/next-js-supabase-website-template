<div align="center">
  <img src="public/MoonrakerDevelopment.png" alt="Next.js + Supabase Template" width="800"/>
  <h1>Next.js 14 + Supabase Website Template</h1>
  <p>🚀 Production-Ready • 🔒 Type-Safe • 💎 Feature-Rich</p>
</div>

<div align="center">
  <a href="#features">Features</a> •
  <a href="#demo">Live Demo</a> •
  <a href="#quick-start">Quick Start</a> •
  <a href="#supabase-features">Supabase Features</a> •
  <a href="#deployment">Deploy</a>
</div>

---

## ✨ Features

- 🏗️ **Next.js 14** - Latest features including App Router and Server Components
- 🔐 **Supabase** - Production-ready backend with:
  - 🔑 Authentication (Email, Social Providers)
  - 📦 Database (PostgreSQL)
  - 🗂️ Storage (Large Media Files)
  - 🔄 Real-time Subscriptions
  - 🚀 Edge Functions
- 🎨 **Modern Stack**:
  - 💅 Tailwind CSS - Utility-first CSS
  - 🧱 shadcn/ui - Re-usable components
  - 🔍 TypeScript - Type safety
  - 📱 Responsive Design
  - 🌐 SEO Optimized

## 🎯 Quick Start

### 1️⃣ Clone & Install

```bash
# Clone the repository
git clone https://github.com/yourusername/next-js-website-template.git

# Navigate to the project
cd next-js-website-template

# Install dependencies
npm install
```

### 2️⃣ Set Up Supabase

1. Create a Supabase project at [supabase.com](https://supabase.com)
2. Copy your project credentials
3. Set up environment variables:
```bash
cp .env.example .env.local
```
4. Fill in your Supabase credentials in `.env.local`

### 3️⃣ Run Development Server

```bash
npm run dev
```

Visit [http://localhost:3000](http://localhost:3000) 🎉

## 🔥 Supabase Features

### Authentication

```typescript
// Sign Up
const { data, error } = await supabase.auth.signUp({
  email: 'user@example.com',
  password: 'password123'
})

// Sign In
const { data, error } = await supabase.auth.signInWithPassword({
  email: 'user@example.com',
  password: 'password123'
})

// Social Auth (GitHub example)
const { data, error } = await supabase.auth.signInWithOAuth({
  provider: 'github'
})
```

### Database Operations

```typescript
// Create
const { data, error } = await supabase
  .from('todos')
  .insert({ task: 'Buy milk', user_id: user.id })

// Read
const { data, error } = await supabase
  .from('todos')
  .select('*')
  .eq('user_id', user.id)

// Update
const { data, error } = await supabase
  .from('todos')
  .update({ completed: true })
  .eq('id', todoId)

// Delete
const { data, error } = await supabase
  .from('todos')
  .delete()
  .eq('id', todoId)
```

### Real-time Subscriptions

```typescript
// Subscribe to changes
const subscription = supabase
  .channel('todos')
  .on('postgres_changes', 
    { event: '*', schema: 'public', table: 'todos' },
    (payload) => {
      console.log('Change received!', payload)
    }
  )
  .subscribe()
```

### File Storage

```typescript
// Upload file
const { data, error } = await supabase.storage
  .from('avatars')
  .upload('public/avatar1.png', file)

// Download file
const { data, error } = await supabase.storage
  .from('avatars')
  .download('public/avatar1.png')
```

## 📁 Project Structure

```
├── src/
│   ├── app/                 # App Router Pages
│   │   ├── (auth)/         # Authentication Routes
│   │   ├── dashboard/      # Protected Routes
│   │   └── page.tsx        # Home Page
│   ├── components/         # React Components
│   │   ├── ui/            # UI Components
│   │   └── auth/          # Auth Components
│   ├── lib/               # Utilities
│   │   ├── supabase.ts    # Supabase Client
│   │   └── utils.ts       # Helper Functions
│   └── types/             # TypeScript Types
├── public/                # Static Assets
└── ...config files
```

## 🔧 Advanced Configuration

### Database Schema

```sql
-- Example schema for a basic todo app
create table public.todos (
  id uuid default uuid_generate_v4() primary key,
  user_id uuid references auth.users not null,
  task text not null,
  completed boolean default false,
  created_at timestamp with time zone default timezone('utc'::text, now())
);

-- Enable Row Level Security
alter table public.todos enable row level security;

-- Create policies
create policy "Users can view their own todos" 
  on todos for select using (auth.uid() = user_id);
```

### Storage Buckets

1. Create a new bucket:
```sql
insert into storage.buckets (id, name)
values ('avatars', 'avatars');
```

2. Set up storage policies:
```sql
create policy "Avatar images are publicly accessible"
  on storage.objects for select
  using ( bucket_id = 'avatars' );

create policy "Users can upload their own avatar"
  on storage.objects for insert
  with check ( bucket_id = 'avatars' AND auth.uid() = owner );
```

## 🚀 Deployment

### Deploy to Vercel

1. Push your code to GitHub
2. Import your repository to Vercel
3. Add your environment variables
4. Deploy!

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/elhard1/next-js-website-template)

### Deploy to Other Platforms

- [Railway](https://railway.app)
- [Netlify](https://netlify.com)
- [DigitalOcean](https://digitalocean.com)

## 📚 Learning Resources

- [Supabase Documentation](https://supabase.com/docs)
- [Next.js Documentation](https://nextjs.org/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [TypeScript Documentation](https://www.typescriptlang.org/docs)

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 💖 Support

If you find this template helpful, please give it a ⭐️ on GitHub and consider:

- [Following me on GitHub](https://github.com/elhard1)
- [Reporting issues](https://github.com/yourusername/next-js-website-template/issues)
- [Contributing to the project](#contributing)

---

<div align="center">
  Made by <a href="https://github.com/elhard1">elhard1</a>
</div>

