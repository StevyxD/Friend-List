# Friends

A simple Rails 8.1 web app for keeping track of your friends' contact info. Sign up, log in, and manage a personal list of contacts — each with a name, email, phone number, and Twitter handle. Records are scoped to the signed-in user, so only the owner can edit or delete their own friends.

## Features

- 🔐 User authentication with [Devise](https://github.com/heartcombo/devise)
- 👥 Full CRUD for friend contacts (first name, last name, email, phone, Twitter)
- 🛡️ Per-user authorization — only the owner can edit or destroy a record
- ⚡ Hotwire (Turbo + Stimulus) for snappy interactions without heavy JS
- 📦 Solid Cache / Solid Queue / Solid Cable — no Redis required

## Tech Stack

| Layer          | Tool                                     |
| -------------- | ---------------------------------------- |
| Framework      | Ruby on Rails 8.1                        |
| Language       | Ruby 3.3.6                               |
| Database       | SQLite                                   |
| Auth           | Devise 5                                 |
| Frontend       | Hotwire (Turbo + Stimulus), Propshaft    |
| Asset bundling | Importmap                                |
| Web server     | Puma behind Thruster                     |
| Deploy         | Kamal + Docker                           |

## Getting Started

### Prerequisites

- Ruby 3.3.6 (see `.ruby-version`)
- Bundler
- SQLite 3 (≥ 2.1)

### Setup

```bash
git clone https://github.com/StevyxD/Friend-List.git
cd Friend-List
bundle install
bin/rails db:setup
bin/rails server
```

Visit [http://localhost:3000](http://localhost:3000) and sign up to start adding friends.

### Running Tests

```bash
bin/rails test         # unit + integration tests
bin/rails test:system  # browser tests via Capybara + Selenium
```

### Security & Linting

```bash
bin/brakeman           # static security analysis
bundle exec bundler-audit check --update
bin/rubocop            # style (rubocop-rails-omakase)
```

## Deployment

A `Dockerfile` and Kamal configuration are included. To deploy with [Kamal](https://kamal-deploy.org):

```bash
bin/kamal setup
bin/kamal deploy
```

## Project Structure

- `app/models/user.rb` — Devise user, owns many friends
- `app/models/friend.rb` — belongs to a user
- `app/controllers/friends_controller.rb` — CRUD with `correct_user` before-action guarding mutations
- `db/migrate/` — schema for users and friends

## License

MIT
