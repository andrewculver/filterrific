---
layout: default
---

<div class="page-header">
  <h1>Filterrific</h1>
</div>



{% include project_navigation.html %}

Filterrific is a Rails Engine plugin that makes it easy to add filtering,
searching, and sorting to your ActiveRecord lists.

It comes with the following features:

* Let your app's users search, filter and sort lists of ActiveRecord objects.
* Add as many AND filter dimensions as you want.
* Persist filter settings in session or DB (for saved searches).
* Integrates with pagination.
* Filters can be reset to default settings.
* Relies on ActiveRecord scopes for building DB queries.
* Comes with the plumbing to shuttle filter settings from a filter UI to
  the controller and ActiveRecord.
* Can be used for JSON/XML/HTML response formats.


<div style="margin: 3em 0;">
  <blockquote>
    <p>
      I couldn't live without Filterrific. It makes it super easy to add
      user configurable reporting to my client projects.
    </p>
    <small>Jeff Ward, Animikii</small>
  </blockquote>
</div>

### How to use it

Let's say you want a list of students that can be filtered by your app's users.

1) Put this code in your `Student` model:

```ruby
  filterrific(
    :default_settings => {
      :sorted_by => 'created_at_desc'
    },
    :filter_names => %w[
      search_query
      sorted_by
      with_country_id
    ]
  )
  # define ActiveRecord scopes for
  # :search_query, :sorted_by, and :with_country_id
```

2) Put this in the `index` action in your `StudentsController`:

```ruby
def index
  @filterrific = Filterrific.new(Student, params[:filterrific])
  @students = Student.filterrific_find(@filterrific).page(params[:page])

  respond_to do |format|
    format.html
    format.js
  end
end
```
3) And finally build this in `app/views/students/index.html.erb`:

<p class="unconstrained">
  <img src="/images/screenshot_u.png" alt="Filterrific in action" class="img-polaroid" />
  <div class="img_caption">
    Example 1: A simple student list that can be filtered.
  </div>
</p>


### Example 2

<p class="unconstrained">
  <img src="/images/screenshot_c.png" alt="Filterrific in action" class="img-polaroid" />
  <div class="img_caption">
    Example 2: Filtering a list of members, with saved searches,
    pagination and filter reset. List at the left, filters to the right.
  </div>
</p>


### Example 3

<p class="unconstrained">
  <img src="/images/screenshot_q.png" alt="Filterrific in action" class="img-polaroid" />
  <div class="img_caption">
    Example 3: Filtering a list of questions. Filters above, list below.
  </div>
</p>


### Details

* Filterrific takes care of shuttling user defined filter settings from your view
  to ActiveRecord queries, and of returning matching records back to the view.
  You are responsible to implement the aspects that are specific
  to your application:
    * define the required scopes
    * style your filter form and record lists
* You use 3 APIs to integrate Filterrific into your app: Model, View and Controller.

This documentation uses an example application to demonstrate usage of each
Filterrific API with lots of example code. Just follow the links at the bottom
of each page:

<p>
  <a href="/pages/example_application.html" class='btn btn-success'>Learn about the example application &rarr;</a>
</p>


### Dependencies

* Rails and ActiveRecord 3.x and 4
* PostgreSQL or MySQL
* Ruby 1.8.7 or greater
* jQuery and Asset pipeline for form observers and spinner



### Installation

`gem install filterrific`

or with bundler in your Gemfile:

`gem 'filterrific'`



### Resources

* [Documentation](http://filterrific.clearcove.ca)
* [Changelog](https://github.com/jhund/filterrific/blob/master/CHANGELOG.md)
* [Source code (github)](https://github.com/jhund/filterrific)
* [Issues](https://github.com/jhund/filterrific/issues)
* [Rubygems.org](http://rubygems.org/gems/filterrific)



### License

[MIT licensed](https://github.com/jhund/filterrific/blob/master/MIT-LICENSE).



### Copyright

Copyright (c) 2010 - 2013 Jo Hund. See [(MIT) LICENSE](https://github.com/jhund/filterrific/blob/master/MIT-LICENSE) for details.

<p>
  <a href="/pages/example_application.html" class='btn btn-success'>Learn about the example application &rarr;</a>
</p>
