---
date: 2021-06-02
title: Context APIs
categories:
  - react
description: Setting up React routers
type: Document
---

Context provides a way to pass data through the component tree without having to pass props down manually at every level.

## Importing and Example

```
import React, {useState,createContext} from "react";

export const RestaurantsContext = createContext();

export const RestaurantsContextProvider = props => {

    const [restaurants, setRestaurants] = useState([]);
    const [selectedRestaurant, setSelectedRestaurant] = useState(null);

    const addRestaurants = (restaurant) => {
        setRestaurants([...restaurants,restaurant]);
    }

    return (
        <RestaurantsContext.Provider value={{restaurants, setRestaurants, addRestaurants, selectedRestaurant, setSelectedRestaurant}}>
            {props.children}
        </RestaurantsContext.Provider>
    )
}
```

`RestaurantsContextProvider` wraps the application so that it has access to our state.

`const [restaurants, setRestaurants] = useState([]);` is an array that fetches the list of restaurants from the backend. setRestaurants allows us to edit restaurants. useState([]) is initially an empty array.

`<RestaurantsContext.Provider>` refers to the provider component. 
`value=({...})` contains a list of objects to be passed into the RestaurantsContext.Provider.