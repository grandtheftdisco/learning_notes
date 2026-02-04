check all css files for trailing whitespace:
`find app/assets/tailwind -name "*.css" -exec sed -i 's/[ \t]*$//' {} \;`

run tests with local .env file
`cd /home/[project_repo] && RAILS_ENV=test bundle exec rails test [path_to_test]`
