# Customer Service Support Technician Tech Test

Test for CS Support candidates

## Requirements

Allowing for setting up the project, this tech test should take around 2 hours to complete.

1. Find the cause of issues in the application:

- There are three bugs to find
- You are not required to _fix_ the bugs, your aim is to **identify** what is causing them

2. Document your process:

- What did you notice/find?
- What are your recommendations?

## Getting Started

These instructions will get the application up and running on your local machine for bug finding purposes.

- Install Ruby [Ways of Installing Ruby](https://www.ruby-lang.org/en/downloads)
- Install Yarn [Ways of Installing Yarn](https://yarnpkg.com/lang/en/docs/install)
- Clone this git repository `git clone git@github.com:smartpension/smart-cs-support-test.git`
- cd into the locally cloned repo `smart-cs-support-test`
- Run `bin/setup`
- Start up your web-server (see the output of `bin/setup`)
- If you get an error with: `getaddrinfo: nodename nor servname provided, or not known (SocketError)`
  - Try running your server with`./bin/rails server -b 0.0.0.0`
- Navigate to: http://localhost:3000

Remember to document **how** you identified the bugs and attach your findings to your email back to us, have fun!!

FINDINGS:

1. Create a new employee
   In app/views/employees/new.html.erb, the form.label is showing a different form.text_field
   An employee needs a forename, middlename and surname and with the current form that is not possible.
   Instead, it should be:

`<%= form.label :forename %> <%= form.text_field :forename, class:
"form-control" %>

 <p>
   <%= form.label :middlename %> <%= form.text_field :middlename, class:
   "form-control" %>
 </p>
 <p>
   <%= form.label :surname %> <%= form.text_field :surname, class:
   "form-control" %>
 </p>`

2. Create a new company
   The create functionality works but it redirects to a different company show page upon creation. This is true for all companies→ the show page is always for Mickeys plaice.
   First I had a look at the show page and then realised that the error was in the company controller. In the show method, it is written that the company is always the first company.
   Instead, it should be:

`def show
@company = Company.find(permitted_params[:id])

# @company = Company.first

end`

3. Edit employees not working on the company show page
   When you click edit, the wrong URL was being made. The company id was the employee id and the employee id was the company id.
   I went to the company show page and saw that @company was not being given to the edit_company_employee_path.
   The code should look like this instead in app/views/companies/show.erb:

`<td>
     <%= link_to "Edit", edit_company_employee_path(@company, employee ),
       class: "btn btn-primary btn-sm" %>
</td>`
