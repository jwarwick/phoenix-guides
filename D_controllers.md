##Controller Guide

Phoenix controllers act as a sort of intermediary modules. Their functions - called actions - are invoked from the router in response to HTTP requests. The actions, in turn, gather all the necessary data and perform all the necessary steps before invoking the view layer to render a template. (Views and templates have their own guides coming up.)

A newly generated Phoenix app will have a single controller, the PageController, which looks like this.

```elixir
defmodule HelloPhoenix.PageController do
  use Phoenix.Controller

  def index(conn, _params) do
    render conn, "index"
  end

  def not_found(conn, _params) do
    render conn, "not_found"
  end

  def error(conn, _params) do
    render conn, "error"
  end
end
```

###Actions
- names and behaviors
  - can be named anything, but for crud apps, there are a set of standard actions which we get from the 'resources' macro in the router.
index - list of all
show - show individual by id
new - generic for presenting form for new thing
create - receives params for one record and creates record in datastore
edit - pulls individual record by id for editing
update - receives params for one edited record and save to datastore
destroy - receives id for record to be deleted and deletes it from datastore

- function signature
  - conn - the connection resource
    - this comes in through the router, the match functions
  - pattern matching of parameters

- gathering data
Phoenix does not currently ship with it's own data access layer, but a number of options are available. Ecto provides very nice data model functionality for those using the Postgres relational database. (Other adapters are coming for Ecto.) Ets and Dets are key value data stores built into OTP which can be queried directly from a controller in Elixir. There is also the mnesia database from otp. This is a relational database with it's own query language, QLC.

- rendering
  - html, the default
  - text
  - json, xml and beyond


def sitemap(conn, _params) do
  conn
  |> put_resp_content_type("text/xml")
  |> render "sitemap"
end


- error pages, 404, 500
- flash messages
  - Flash module
  - set and get functions
