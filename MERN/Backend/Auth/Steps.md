
### 1. REGISTER -
- save user details in db
- make sure to `hash` password ( don't save password directly into db )
- ```js
  const hashPass = await bcrypt.hash(password, 10);
  ```

### 2. LOGIN -
- take gmail  and password from user with request
- find the user in db using gmail.
- compare the password given and the stored hashed password in db
- if same -> generate JWT token        {   `it uses jwt.sign() method` }
- send token as response
- ```js
      const user = await User.findOne({ email });

    if(user && (await bcrypt.compare(password, user.password))){

        const accessToken = jwt.sign({

            user: {

                username: user.username,

                email: user.email,

                id: user.id

            }

        },

        process.env.ACCESS_TOKEN_SECRET,

        {expiresIn: '15m'}

    );
            res.status(200).json({accessToken});

    }
  ```

### 3. GET CURRENT USER -
- add a middleware to before endpoint
  ```js
  router.route('/current').get(validateToken, currentUser);
  ```
- this middleware will validate if the user is logged in
- HOW IT VALIDATES -
  1. the bearer access token is sent with request in `authorization` field.
  2. now it will verify the token with the `key` it used during it's invention. { by `jwt.verify()`  }
  3. ```js
             jwt.verify(token,process.env.ACCESS_TOKEN_SECRET, (err, decoded) => {

            if(err){

                res.status(401);

                throw new Error('User is not authorized');

            }

            console.log('Decoded token: ', decoded);

            req.user = decoded.user; // this will be available in the next middleware or controller function
            // it is currentUser controller in this case

            next();

        });
     ```
     - At last, if verification is successful, the required info will be in the `decoded`.
     - it shall be passed to the next middleware or controller.  ( so set `request` as the data )
     - now when the control is passed to the `currentUser` controller, it have required data in the request itself.
     - so controller just send response as the `req.user`



