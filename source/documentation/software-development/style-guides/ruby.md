# Ruby

## Style guide

Our Ruby style guide is enforced by [RuboCop] with [rubocop-govuk] imported.

## Testing with RSpec

We test our Ruby code using RSpec

### Contents

* [What do we use RSpec for?](#what-do-we-use-rspec-for)
* [Why RSpec?](#why-rspec)
* [How to configure RSpec](#how-to-configure-rspec)
* [Example unit test](#example-unit-test)
* [Example integration test](#example-integration-test)

### What do we use RSpec for?

We use RSpec to write both unit and integration tests for Ruby code.

### Why RSpec?

[RSpec is the most popular test framework for Ruby][ruby-toolbox], and is [recommended for Rails][gorails].

This explains why we use RSpec for our unit tests. For integration tests, there is another popular alternative to RSpec, and that is Cucumber.

Many GOV.UK applications have some or all of their integration tests written in Cucumber. However, we are gradually moving away from Cucumber in favour of using RSpec, for reasons outlined in this article: [How we write readable feature tests with RSpec][chris-zetter-blogpost].

Essentially, using RSpec for both BDD and TDD requires less of a context switch than using a separate tool for BDD.

[ruby-toolbox]: https://www.ruby-toolbox.com/categories/testing_frameworks
[gorails]: https://gorails.com/tool_categories/test-frameworks/tools
[chris-zetter-blogpost]: https://about.futurelearn.com/blog/how-we-write-readable-feature-tests-with-rspec

### How to configure RSpec

We should try to avoid the pollution of the global namespace that came with earlier versions of RSpec. For example, we should be using `RSpec.describe` instead of `describe`.

This can be enforced by setting `config.expose_dsl_globally = false` in your test setup. Read [Global namespace DSL][Global namespace DSL] for more information.

[Global namespace DSL]: https://relishapp.com/rspec/rspec-core/docs/configuration/global-namespace-dsl

### Example unit test

This example is taken from [finder-frontend][finder-frontend]:

[finder-frontend]: https://github.com/alphagov/finder-frontend

```ruby
RSpec.describe ContentItem do
  subject { described_class.new(base_path) }
  let(:base_path) { "/search/news-and-communications" }
  let(:finder_content_item) { news_and_communications }
  let(:news_and_communications) {
    JSON.parse(File.read(Rails.root.join("features", "fixtures", "news_and_communications.json")))
  }

  RSpec.describe "as_hash" do
    it "returns a content item as a hash" do
      expect(subject.as_hash).to eql(finder_content_item)
    end
  end
end
```

### Example integration test

This example is taken from [publishing-e2e-tests][publishing-e2e-tests]:

[publishing-e2e-tests]: https://github.com/alphagov/publishing-e2e-tests

```ruby
# Some methods and variables have been removed here for brevity, but you get the idea.

RSpec.feature "Publishing a parent and child topic on Collections Publisher" do
  let(:parent_title) { unique_title }
  let(:child_title) { unique_title }

  RSpec.scenario "Publishing a parent and child topic" do
    given_i_have_a_published_topic
    when_i_add_a_child_topic
    and_i_publish_it
    then_i_can_view_both_on_gov_uk
  end

private

  def signin_to_signon
    signin_with_next_user("Collections Publisher" => ["GDS Editor"])
  end

  def then_i_can_view_both_on_gov_uk
    click_link(link)
    expect_url_matches_live_gov_uk
    expect(page).to have_content(child_title)

    first(:link, parent_title).click
    expect_url_matches_live_gov_uk
    expect(current_url).to end_with(parent_slug)
  end
end
```

[RuboCop]: https://github.com/rubocop-hq/rubocop 
[rubocop-govuk]: https://github.com/alphagov/rubocop-govuk