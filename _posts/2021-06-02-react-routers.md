---
date: 2021-06-02
title: React Router Setup
categories:
  - react
description: Setting up React routers
type: Document
---

## Installation
npm install react-router-dom

Create a routes folder to place routes in.

Use the 'rafce' keyword to quickly set up a code template for a react router.

`import {BrowserRouter as Router, Switch, Route} from "react-router-dom"`

## Creating the Route

Surround the content with `<Router> </Router>` tags and surround those with `<Switch> </Switch>` tags. The Switch tags tell the app which component to load based on what route was selected.

Inside those tags, `<Route exact path="/[page name]" component={Component}/>` where [page name] is the name of the page and Component is the component to be loaded in the router.

In the case of a home page, leave the path as "/".

Be sure to import those routes from the route folder. 