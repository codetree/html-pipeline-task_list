# frozen_string_literal: true

# rspec configuration
minitest_opts = {
  cmd: 'rake test',
  autorun: false,
  all_on_start: true
}

rubocop_opts = {
  all_on_start: true,
  cli: ['--display-cop-names']
}

shell_opts = {
  all_on_start: true
}

group :rails, halt_on_fail: true do
  guard :minitest, minitest_opts do
    directories %w[test lib]
    watch %r{^test/(.+)_test\.rb$}
    watch(%r{^lib/(.+)\.rb$}) { |m| "test/#{m[1]}_test.rb" }
  end

  guard :rubocop, rubocop_opts do
    directories %w[test lib]
    watch(%r{^test/.+\.rb$})
    watch(%r{^lib/(.+)\.rb$})
  end

  # run js tests
  guard :shell, shell_opts do
    directories %w[test app]
    watch(%r{^app/(.+)\.js$}) { `npm test` }
  end

  # run linting
  guard :shell, shell_opts do
    directories %w[test app]
    watch(%r{^app/(.+)\.js$}) { `npm run lint` }
  end
end
