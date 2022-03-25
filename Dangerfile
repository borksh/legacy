# frozen_string_literal: true

# Warn when a PR is classed as work in progress
warn 'PR is classed as Work in Progress' if github.pr_title.downcase.include? '(wip)'

# Note when a PR cannot be manually merged, which goes away when you can
can_merge = github.pr_json['mergeable']
warn('This PR cannot be merged yet.', sticky: false) unless can_merge

labels_to_add = []
labels_to_add << 'enhancement' if github.pr_title.include? '(feature)'
labels_to_add << 'bug' if github.pr_title.include? '(bug)'
github.api.add_labels_to_an_issue github.pr_json[:base][:repo][:full_name], github.pr_json[:number], labels_to_add

# GitHub Review section
github.review.start

# Ensure there is a summary for a PR
github.review.fail 'Please provide a summary in the Pull Request description' if github.pr_body.length < 5

# Check that there are both app and test code changes for the main app
CHANGED_FILES = (git.added_files + git.modified_files).freeze
changed_app_files = CHANGED_FILES.select { |path| path =~ /^types/ }
if changed_app_files.any?
  changed_test_files = CHANGED_FILES.select { |path| path =~ /^test/ }
  if changed_test_files.empty?
    github.review.warn "Are you sure we don't need to add/update tests?"
  end
end

github.review.submit