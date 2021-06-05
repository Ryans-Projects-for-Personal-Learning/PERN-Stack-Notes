---
date: 2021-05-23
title: Express Routes
categories:
  - express
description: Creating routes with Express
type: Document
order_number: 1
---
## About

Routing refers to determining how an application responds to a client request to a particular endpoint, which is a URI (or path) and a specific HTTP request method (GET, POST, and so on).

## HTTP Request Methods
* Get: Retrieves requested data from a resource.
* Post: Submits data to a resource.
* Put: Updates a specified resource.
* Delete: Removes the specified resource.

## Syntax

let `const app = express()`. Then to create a route.

app.[http method]("/api/v1/...", async (req, res) => {
    const results = await db.query([sql query]);
    res.status([number]);
});

## Examples

Examples of routes using a restaurants database

### Get All Restaurants

```
app.get("/api/v1/restaurants", async (req,res) => {
    
    try{
        //const results = await db.query("SELECT * FROM RESTAURANTS");
        const restaurantRatingData = await db.query("SELECT * FROM restaurants left join (select restaurant_id, COUNT(*), TRUNC(AVG(rating),1) as average_rating from reviews group by restaurant_id) reviews on restaurants.id = reviews.restaurant_id;"
        );
        res.status(200).json({
        status: "success",
        results: restaurantRatingData.rows.length,
        data: {
            restaurants: restaurantRatingData.rows,
        },
    });
    } catch (err){
        console.log(err);
    }

});
```

### Get One Restaurant
```
app.get("/api/v1/restaurants/:id", async(req, res) => {
    console.log(req.params);

    try {
        const restaurant = await db.query("SELECT * FROM restaurants left join (select restaurant_id, COUNT(*), TRUNC(AVG(rating),1) as average_rating from reviews group by restaurant_id) reviews on restaurants.id = reviews.restaurant_id where id=$1;", [req.params.id]
        );

        const reviews = await db.query("select * from reviews where restaurant_id = $1", [req.params.id,]);

        res.status(200).json({
            status: "success",
            data: {
                restaurant: restaurant.rows[0],
                reviews: reviews.rows,
            },
        });

    } catch (err){
        console.log(err);
    }
    
    
});
```

### Create a Restaurant
```
app.post("/api/v1/restaurants", async (req, res) => {
    console.log(req.body);

    try{
        const results = await db.query("INSERT INTO restaurants (name, location, price_range) values ($1, $2, $3) returning *", [req.body.name,req.body.location,req.body.price_range])
        console.log(results);
        res.status(201).json({
            status: "success",
            data: {
                restaurant: results.rows[0],
            }
        })
    } catch {
        console.log(err);
    }
    
});
```

### Update a Restaurant
```
app.put("/api/v1/restaurants/:id", async (req, res) => {
    try{
        const results = await db.query("UPDATE restaurants SET name = $1, location = $2, price_range = $3 where id = $4 returning *", [req.body.name,req.body.location,req.body.price_range, req.params.id]);

        res.status(200).json({
            status: "success",
            data: {
                restaurant: results.rows[0],
            }
        })
        console.log(results);
    } catch (err) {
        console.log(err);
    }
    
    console.log(req.params.id);
    console.log(req.body);
    
});
```

### Delete a Restaurant
```
app.delete("/api/v1/restaurants/:id", async (req,res) => {
    try {
        const results = await db.query("DELETE FROM restaurants where id = $1",[req.params.id]);
        res.status(204).json({
            status: "success",
        })
    } catch (err){
        console.log(err);
    }
    
});
```

## Route Naming Convention

"/api/v1/.../"

If you need a particular entry in a table, attach a /:id at the end.