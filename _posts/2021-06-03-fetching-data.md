---
date: 2021-06-03
title: Fetching and Reendering Data
categories:
  - react
description: Fetch data from the backend to update the front end
type: Document
order_number: 1
---

## Getting Started

Create a directory called "apis" in the client folder. Then import axios.

Then create a base url.

```
import axios from "axios";

export default axios.create({
    baseURL: "http://localhost:4000/api/v1/restaurants",
})
```

## Components
Edit the component so that it fetches the data from the backend using `UseEffect`

### Example

```
useEffect( () => {
        const fetchData = async () => {
            try {
                const response = await RestaurantFinder.get("/")
                setRestaurants(response.data.data.restaurants);
             } catch (err){
                 
             }
        };

        fetchData();

        
    }, []);
```

## Rendering Data

```
 return (
        <div className="list-group">
            <table className="table table-hover table-dark">
                <thead>
                    <tr className="table bg-primary">
                        <th scope="col">Restaurant</th>
                        <th scope="col">Location</th>
                        <th scope="col">Price Range</th>
                        <th scope="col">Rating</th>
                        <th scope="col">Edit</th>
                        <th scope="col">Delete</th>
                    </tr>
                </thead>
                <tbody>
                    {restaurants && restaurants.map(restaurant => {
                        return (
                        <tr onClick={() => handleRestaurantSelect(restaurant.id)} key={restaurant.id}>
                            <td>{restaurant.name}</td>
                            <td>{restaurant.location}</td>
                            <td>{"$".repeat(restaurant.price_range)}</td>
                            <td>{renderRating(restaurant)}</td>
                            <td><button onClick={(e) => handleUpdate(e, restaurant.id)} className = "btn btn-warning">Update</button></td>
                            <td><button onClick={(e) => handleDelete(e, restaurant.id)} className = "btn btn-danger">Delete</button></td>
                        </tr>
                        )
                    })}
                    
                
                </tbody>
            </table>
        </div>
    )
```