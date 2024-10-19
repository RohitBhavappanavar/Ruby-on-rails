# Ruby on rails
# Use the official Ruby image as the base
FROM ruby:3.2

# Install dependencies
RUN apt-get update -qq && apt-get install -y \
    build-essential libpq-dev nodejs postgresql-client

# Set the working directory
WORKDIR /app

# Copy Gemfile and Gemfile.lock to the container
COPY Gemfile Gemfile.lock ./

# Install Ruby gems
RUN bundle install

# Copy the entire project to the container
COPY . .

# Expose port 3000 for Rails
EXPOSE 3000

# Start the Rails server
CMD ["bundle", "exec", "rails", "server", "-b", "0.0.0.0"]
