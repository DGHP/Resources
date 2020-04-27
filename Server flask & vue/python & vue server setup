### Intro

Below is a simplified version of the first section of <https://testdriven.io/blog/developing-a-single-page-app-with-flask-and-vuejs/>.

Things to note:
- make sure both your python flask server and vue application are running 
- in vue we'll use an npm package called axios to do the equivalent of JS fetch


## Setting up router in vue with flask

Globall installation of @vue/cli didn't work. Instead I created a vue app using npx @vue/cli create --default my-project.

When creating the app make sure to use default setup and add router. 

Vue can thrown funny errors such as newline empty char missing, this will happen if you choose ro add lint onto the project when setting up.


## set up flask environment

1. Create a server directory in your project directory
2. In your console run : 
```
 python3.7 -m venv env
$ source env/bin/activate
```
3. You should now see ```(env)``` at the beggining of the new line in the terminal
4. Install Flask-CORS using pip
```
(env)$ pip install Flask==1.0.2 Flask-Cors==3.0.7
```

5. create app.py 

```python=
from flask import Flask, jsonify
from flask_cors import CORS


# configuration
DEBUG = True

# instantiate the app
app = Flask(__name__)
app.config.from_object(__name__)

# enable CORS
CORS(app, resources={r'/*': {'origins': '*'}})


# sanity check route
@app.route('/route_name', methods=['GET'])
def your_route_name():
    return jsonify('some response')
#     here's what is going to be returned from your route 


if __name__ == '__main__':
    app.run()
```
6. inside of the server folder run pyton app.py to start the server

## To access the above route in your vue application : 

1. Crate a new component, make sure axios dependency is installed then use it inside of the given component to get the response from our server 

router.js
```javascript=
import Vue from 'vue';
import Router from 'vue-router';
import YourComponent from './components/YourComponent.vue';

Vue.use(Router);

export default new Router({
  mode: 'history',
  base: process.env.BASE_URL,
  routes: [
    {
      path: '/your-path',
      name: 'YourComponent',
      component: YourComponent,
    }
  ],
});
```

YourComponent.vue
```javascript=
<script>
import axios from 'axios';

export default {
  name: 'YourComponent',
  data() {
    return {
      msg: '',
    };
  },
  methods: {
    getMessage() {
      const path = 'http://path_on_which_your_python_server_is_running/route_name';
      axios.get(path)
        .then((res) => {
          this.msg = res.data;
        })
        .catch((error) => {
          // eslint-disable-next-line
          console.error(error);
        });
    },
  },
  created() {
    this.getMessage();
  },
};
</script>
```

2. Running your vue app should now get connected to your python server


