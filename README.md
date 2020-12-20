#### Android App Development Lab

# Project Title : Bh WhatsApp Community Analyzer 

### Members:  
Shaun Misquitta 42  
Sanika Bhagwat 03  
Tanmay Joshi 27   


## Tech Stack 

FrontEnd - React Native     
Backend - Nodejs, Express,Mongodb , JWT (Authentication)

## Frontend Code Snippet for Login Screen
```
render(){
        return(
            <View style={styles.body}>
                <View style={styles.container}>
                    <Text style={styles.login_heading}>Login</Text>
                    <Text style={styles.email_add_text}>Email address</Text>
                    <TextInput autoCapitalize='none' style={styles.username_input} onChangeText={(val)=> this.setState({email:val})}></TextInput>

                    <Text  style={styles.password_text}>Password</Text>
                    <TextInput  autoCapitalize='none' secureTextEntry={true} style={styles.password_input}  onChangeText={(val)=> this.setState({password:val})}></TextInput>
                    
                    <TouchableOpacity style={styles.login_btn_shape} onPress={() => this.onsubmit()}>
                        <AD style={styles.login_btn_arrowname} name='arrowright' color='white' size={20}/>
                       
                    </TouchableOpacity>

                    <Text style={styles.new_mem_text}>New Team Member?</Text>
                    

                    <TouchableOpacity style={styles.sign_up_btn} onPress={()=>this.props.navigation.navigate('Signup')}>
                        <View style={styles.sign_up_con}>
                            <Text style={styles.sign_up_text}>SIGN UP</Text>
                        
                            <AD style={styles.sign_up_arrow} name='caretright' color='#000000' size={10}/>
                        </View>
                    </TouchableOpacity>
                </View>
               
            </View> 
           
        )
    }}

```

## Backend Code Snippet for Logging in Users

```
router.post("/login",async(req,res) => {

    const userdata = {
        email :req.body.email,
        password : req.body.password,
        
       }
 
    //Check Existing User
    user.findOne({email: userdata.email})
    .then(user =>{
        var data = user
        if(!user) return res.status(400).json('Not Foundd');
        //If user is Present Validate Password
        bcrypt.compare(userdata.password,user.password)
        .then(ismatch =>{
            if(!ismatch) return res.status(400).json('Password is Incorrect')
            let token = jwt.sign({id:user.id},secretkey)
            res.json({user_details:user,token:token})  
        
        }).catch(err => res.json(err))
    })
    .catch(err => res.json(err))
})
```
