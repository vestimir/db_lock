# DBLock

Gem to obtain and release manual mysql db locks. This can be utilized for example to make sure that certain rake tasks do not run in parallel on the same database (for example when cron jobs run for too long or are accidentally started multiple times).

## Installation

Add this line to your application's Gemfile:

    gem 'db_lock'

then run `bundle`

## Usage

```ruby
DBLock::Lock.get('name_of_lock', 5) do
  # code here
end
```

Before the code block is executed, it will attempt to acquire a mysql db lock for X seconds (5 in this example). If this fails it will raise an `DBLock::AlreadyLocked` error. The lock is released after the block is executed, even if the block raised an error itself.

## Smart lock name

If you prefix the lock with a `.` in a Rails application, `.` will be automatically replaced with `YourAppName.`.
