# LOGIN-PAGE
## AIM:
To create a Login form using React with form validation and password visibility toggle functionality. The form ensures that users enter valid credentials, provides real-time feedback on errors, and displays success or failure messages using toast notifications.

## PROCEDURE:

STEP1: Setup React Environment
Install React (npx create-react-app)
Install React-Toastify for notifications

STEP2: Design Login Component:

Import React, state hooks (useState), and Toastify components.
Import FaEye and FaRegEyeSlash from React Icons to handle password visibility toggling.


STEP 3: Create state variables using useState
email for storing the entered email.
password for storing the entered password.
errors for storing validation error messages.
showPassword to toggle password visibility.


STEP 4:Validation Logic
Validate the following when the form is submitted:
Email field is not empty.
Password field is not empty and is at least 6 characters long.
If the credentials are correct (email: asw393@gmail.com and password: 20022004), display a success toast and redirect to the dashboard after 4 seconds.

STEP 5:Handle Password Visibility:
Use a boolean state (showPassword) to toggle between password and text input types using an icon.

## PROGRAM:
```
import React, { useState } from 'react';
import './Login.scss';
import { ToastContainer, toast } from 'react-toastify';
import 'react-toastify/dist/ReactToastify.css';
import { FaEye, FaRegEyeSlash } from "react-icons/fa";

const Login = () => {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [errors, setErrors] = useState({ email: '', password: '' });
  const [showPassword, setShowPassword] = useState(false);

  const handleSubmit = (e) => {
    e.preventDefault();
    const newErrors = { email: '', password: '' };
    let valid = true;

    if (email === '') {
      newErrors.email = 'Email is required';
      valid = false;
    }

    if (password === '') {
      newErrors.password = 'Password is required';
      valid = false;
    } else if (password.length < 6) {
      newErrors.password = 'Password must be at least 6 characters long';
      valid = false;
    }

    setErrors(newErrors);

    if (valid) {
      if (email === 'asw393@gmail.com' && password === '20022004') {
        toast.success('Form submitted successfully');
        console.log('Form submitted successfully');
        
        setTimeout(() => {
          window.location.href = '/Dashboard';  // Replace with useNavigate for SPA
        }, 4000);
      } else {
        toast.error('Invalid email or password');
      }
    } else {
      toast.error('Please correct the highlighted errors.');
    }
  };

  const toggleVisibility = () => {
    setShowPassword(!showPassword);
  };

  return (
    <div className="container">
      <div className="total-wrap">
        <h1>Login</h1>
        <form onSubmit={handleSubmit}>
          <div className="form-group">
            <label htmlFor="email">Email</label>
            <input
              type="email"
              id="email"
              value={email}
              onChange={(e) => setEmail(e.target.value)}
              required
            />
            <span style={{ color: 'red' }}>{errors.email}</span>
          </div>

          <div className="form-group">
            <label htmlFor="password">Password</label>
            <div className="password-wrapper">
              <input
                type={showPassword ? 'text' : 'password'}
                id="password"
                value={password}
                onChange={(e) => setPassword(e.target.value)}
                required
              />
              <span
                onClick={toggleVisibility}
                style={{ cursor: 'pointer', marginLeft: '8px' }}
                aria-label={showPassword ? "Hide password" : "Show password"}
              >
                {showPassword ? <FaEye /> : <FaRegEyeSlash />}
              </span>
            </div>
            <span style={{ color: 'red' }}>{errors.password}</span>
          </div>

          <button type="submit">Submit</button>
          <ToastContainer />
        </form>

        <a href="#">Sign up</a>
      </div>
    </div>
  );
};

export default Login;
```
## Result:
Thus the programme was executed successfully 
