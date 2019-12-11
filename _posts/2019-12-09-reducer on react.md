---
layout: post
title: Catatan pembelajaran reducer dan provider di react
date: 2019-12-09 10:46
category: react
author: Wahyu Setiawna
tags: [react, mobile, js]
summary: membuat reducer dan provider di react native
---

membuat file reducer dengan naman createDataContext.js, isi file yang akan di gunakan seperti dibawah ini

<pre>
import React, { useReducer } from 'react';

export default ( reducer, action, initialState ) => {
    const Context  = React.createContext();


    const Provider = ({children}) =>{
        const [ state, dispatch ] = useReducer(reducer, initialState);

        return (
            <Context.Provider value={{ state }}>
                {children}
            </Context.Provider>
        );
    }
};
</pre>

isi file di context pusat :

<pre>
import React, { useReducer } fron 'react';
import reactDataContext()

const blogReducer = (state, action) => {
    switch (action.type){
        case "add_blogpost":
        return [...state, { title: 'Blog Post #${state.length + 1}}];
    default:
        return state;
    }
};

const addBlogPost = () => {
    dispatch({ type: 'add_blogpost' });
};

export const { Context, Provider } = createDataContext(blogReducer, { addBlogPost }, [] );
</pre>

<h3>Automatic Context Creation</h3>

menambah automatic content creation dengan menggunakan, mengubah file createDataContext.js, dengan menambahkan beberapa insert dari

<pre>
import React, { useReducer } from 'react';

export defaul ( reducer , action, initialState ) => {
const Context = React.createContext();

    const [ state, dispatch ] = userReducer(reducer, initialReducer);

    const Provider = ({ children }) => {
        const [ state, dispatch ] = userReducer(reducer, initialState );

        const boundsAction = {};

        for (let key in actions){
            boundsAction[key] = actions[key](dispathc);
        }

        return (
            <Context.Provider value=({ state, ...boundsAction })>
                {children}
            </Context.Provider>
        )
    }
}
</pre>

mengubah di index screen dengan menggunakan creation context yang telah di gunakan

<pre>

import React, { userContext } from 'react';
import { View, Text, StyleSheet, FlatList, Button } form 'react-native';
import { Context } form '../context/BlogContext';

const IndexScreen = () => {
const {data, addBlogPost } = userContext(Context);

    return (
        <View>
            <Text>Index Screen</Text>
            <Button title="Add Post" onPress={addBlogPost}/>
            <FlatList
                data={data}
                keyExtractor={blogPost => BlogPost.title}
                renderItem={ ({ item })  => {
                    return <Text>{item.title}</Text>
                }}
            />
        </View>
    )

}
</pre>

<h3>Deleting Post</h3>

untuk menghapus post yang terdapat dalam provider porvider harus dirombah dengan menambahkan beberapa syntaq seperti

<pre>
import React, { useReducer } fron 'react';
import reactDataContext()

const blogReducer = (state, action) => {
    switch (action.type){
        case "delete_blogpost":
            return state.filter({item} => item.id !== action.payload);
        case "add_blogpost":
            return [...state, { title: 'Blog Post #${state.length + 1}}];
        default:
            return state;
    }
};

const addBlogPost = dispatch => {
    return () => {
        dispatch({ type: 'add_blogpost' });
    };
};

const deleteBlogPost = dispatch => {
    return (id) => {
        dispatch({ type: 'delete_blogpost', payload: id});
    };
}

export const { Context, Provider } = createDataContext(blogReducer, { addBlogPost, deleteBlogPost }, [] );
</pre>
/\*

view

\*/

<pre>

import React, { userContext } from 'react';
import { View, Text, StyleSheet, FlatList, Button, TouchableOpacity } form 'react-native';
import { Context } form '../context/BlogContext';
import { Rather } form @expo/vector-icons;

const IndexScreen = () => {
const {data, addBlogPost, deleteBlogPost } = userContext(Context);

    return (
        <View>
            <Text>Index Screen</Text>
            <Button title="Add Post" onPress={addBlogPost}/>
            <FlatList
                data={data}
                keyExtractor={blogPost => BlogPost.title}
                renderItem={ ({ item })  => {
                    return
                        <View>
                            <Text>{item.title} - {item.id}</Text>
                            <TouchableOpacity onPress={() => deleteBlogPost()}>
                                <Father style={styles.icon} name="Trash"/>
                            </TouchableOpacity>
                        </View>;
                }}
            />
        </View>
    )
}
</pre>

<h3>Add Navigation Options</h3>

Header Navigation ditabahkan di file IndexScreen

<pre>

const IndexScreen = () => {
const {data, addBlogPost, deleteBlogPost } = userContext(Context);

    return (
        <View>
            <Text>Index Screen</Text>
            <Button title="Add Post" onPress={addBlogPost}/>
            <FlatList
                data={data}
                keyExtractor={blogPost => BlogPost.title}
                renderItem={ ({ item })  => {
                    return
                        <View>
                            <Text>{item.title} - {item.id}</Text>
                            <TouchableOpacity onPress={() => deleteBlogPost()}>
                                <Father style={styles.icon} name="Trash"/>
                            </TouchableOpacity>
                        </View>;
                }}
            />
        </View>
    )
}

IndexScreen.navigationOptions = (navigation) => {
    return {
    headerRight: <TouchableOpacity onPress={() => navigation.navigate("create")}>
    <Feather name="plus" size={30} />
        </TouchableOpacity>
    }
};
</pre>

<h3>Saving A new post</h3>


<pre>
import React, { useReducer } fron 'react';
import reactDataContext()
import Math from 'math';

const blogReducer = (state, action) => {
    switch (action.type){
        case "delete_blogpost":
            return state.filter({item} => item.id !== action.payload);
        case "add_blogpost":
            return [ ...state, {
                id: Math.floor(Math.random() * 99999),
                title: action.payload.title,
                content: action.payload.content
            } } ];
        default:
            return state;
    }
};

const addBlogPost = dispatch => {
    return (title, content) => {
        dispatch({ type: 'add_blogpost', data: [ title, content ] });
    };
};

const deleteBlogPost = dispatch => {
return (id) => {
    dispatch({ type: 'delete_blogpost', payload: id});
};
}

export const { Context, Provider } = createDataContext(blogReducer, { addBlogPost, deleteBlogPost }, [] );


</pre>


<h2>
catatan untuk bounds actions
</h2>

<pre>
//actions ==== { addBlogPost : (Dispatch) => {return () => {} } }
const boundsActions = {};
fot (let key in actions){
    boundsActions[key] = actions[key](dispatch);
}
</pre>
