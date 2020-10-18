---
layout: post
title:      "My Take on Spotify"
date:       2020-10-18 21:33:14 +0000
permalink:  my_take_on_spotify
---

![](https://yt3.ggpht.com/FSzSzyutwUV9B7uYCpvELTUSNhS5qmc3HqjqmJr1r14V7gKT3N5GxLWKRkdx7s_GfX52Pr7KP7Q=s900-c-k-c0x00ffffff-no-rj)

## Are we really almost there?

I can't believe we are really at the end of this program?! It has been such an intense whirlwind of information that the months have truly flown by. 
This last project was a good challenge for me, incorporating a Rails backend with a React/Redux frontend. I decided with my background in music to take on Spotify, my favorite of the current app market. 


## Utilizing Redux and reducers
The transfer to React and Redux, though intense, felt clear coming from our background in JS. The similarity in `fetch()`  requests within Redux action especially felt familiar. The reducers take in an initial state and as action as arguments and then it returns a copy an updated version of the state, depending on the action type. 


Because I wanted to be able to access and update state information about the artists and songs, as well as playlists, I used `combineReducers()` to create a `rootReducer`. This grants my artists, songs and playlists access to the Redux store: 

```
import { combineReducers } from 'redux'
import artists from './ArtistsReducer'
import songs from './SongsReducer'
import playlists from './PlaylistsReducer'


const rootReducer = combineReducers({
    artists,
    songs,
    playlists
}) 

export default rootReducer
```

## Putting it all together
It felt really fulfilling to create many container and presentational components. To have them work together in such a manner was wonderful. Features like my add and delete buttons, as well as my navbar, were so easy to put together, as they didn't need state and thus took a lot less time to make. Below is my simple add button:
```
import React from 'react'
import { useHistory } from 'react-router-dom'

const AddButton = props => {
  const history = useHistory()
  return (
    <button id="add-button" onClick={() => history.push("/playlists/new")}>{props.name}</button>
  )
}

export default AddButton
```

