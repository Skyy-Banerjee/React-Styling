# Styled Components

```js
import { useState } from 'react';
import { styled } from 'styled-components';

//Styled Components - Tagged Literals
//Actually, components
const ControlledContainer = styled.div`
display: flex;
flex-direction: column;
gap: 0.5rem;
margin-bottom: 1.5rem;
`

const Label = styled.label`
  display: block;
  margin-bottom: 0.5rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: ${({ $invalid }) => ($invalid ? '#f87171' : '#6b7280')};
`
const StyledInput = styled.input`
  width: 100%;
  padding: 0.75rem 1rem;
  line-height: 1.5;
  background-color:${({ $invalid }) => ($invalid ? '#fed2d2' : '#d1d5db')} ;
  color: ${({ $invalid }) => ($invalid ? '#ef4444' : ' #374151')};
  border: ${({ $invalid }) => ($invalid ? '1px solid #f73f3f' : '1px solid transparent')};
  border-radius: 0.25rem;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
`

const StyledBtn = styled.button`
  padding: 1rem 2rem;
  font-weight: 600;
  text-transform: uppercase;
  border-radius: 0.25rem;
  color: #1f2937;
  background-color: #f0b322;
  border-radius: 6px;
  border: none;

  //Psudo stuff:
  &:hover{
    background-color: #f0920e;
  }
`

export default function AuthInputs() {
  const [enteredEmail, setEnteredEmail] = useState('');
  const [enteredPassword, setEnteredPassword] = useState('');
  const [submitted, setSubmitted] = useState(false);

  function handleInputChange(identifier, value) {
    if (identifier === 'email') {
      setEnteredEmail(value);
    } else {
      setEnteredPassword(value);
    }
  }

  function handleLogin() {
    setSubmitted(true);
  }

  const emailNotValid = submitted && !enteredEmail.includes('@');
  const passwordNotValid = submitted && enteredPassword.trim().length < 6;

  return (
    <div id="auth-inputs">
      <ControlledContainer>
        <p>
          <Label $invalid={emailNotValid}>Email</Label>
          <StyledInput
            type="email"
            // className={emailNotValid ? 'invalid' : undefined}
            $invalid={emailNotValid}
            onChange={(event) => handleInputChange('email', event.target.value)}
          />
        </p>
        <p>
          <Label $invalid={passwordNotValid}>Password</Label>
          <StyledInput
            type="password"
            // className={passwordNotValid ? 'invalid' : undefined}
            $invalid={passwordNotValid}
            onChange={(event) =>
              handleInputChange('password', event.target.value)
            }
          />
        </p>
      </ControlledContainer>
      <div className="actions">
        <button type="button" className="text-button">
          Create a new account
        </button>
        <StyledBtn onClick={handleLogin}>Sign In</StyledBtn>
      </div>
    </div>
  );
}
```

```js 
import React from 'react';
import { styled } from 'styled-components';

const Label = styled.label`
  display: block;
  margin-bottom: 0.5rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: ${({ $invalid }) => ($invalid ? '#f87171' : '#6b7280')};
`;

const StyledInput = styled.input`
  width: 100%;
  padding: 0.75rem 1rem;
  line-height: 1.5;
  background-color: ${({ $invalid }) => ($invalid ? '#fed2d2' : '#d1d5db')};
  color: ${({ $invalid }) => ($invalid ? '#ef4444' : '#374151')};
  border: ${({ $invalid }) => ($invalid ? '1px solid #f73f3f' : '1px solid transparent')};
  border-radius: 0.25rem;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
`;

export default function CustomInput({ label, $invalid, ...props }) {
    return (
      <div> {/* Replace <p> with <div> */}
        <Label $invalid={$invalid}>{label}</Label>
        <StyledInput $invalid={$invalid} {...props} />
      </div>
    );
  }
```

```javascript 
import { useState } from 'react';
import { styled } from 'styled-components';
import CustomInput from './Input';
import StyledBtn from './Button';

//Styled Components - Tagged Literals
//Actually, components
const ControlledContainer = styled.div`
display: flex;
flex-direction: column;
gap: 0.5rem;
margin-bottom: 1.5rem;
`
export default function AuthInputs() {
  const [enteredEmail, setEnteredEmail] = useState('');
  const [enteredPassword, setEnteredPassword] = useState('');
  const [submitted, setSubmitted] = useState(false);

  function handleInputChange(identifier, value) {
    if (identifier === 'email') {
      setEnteredEmail(value);
    } else {
      setEnteredPassword(value);
    }
  }

  function handleLogin() {
    setSubmitted(true);
  }

  const emailNotValid = submitted && !enteredEmail.includes('@');
  const passwordNotValid = submitted && enteredPassword.trim().length < 6;

  return (
    <div id="auth-inputs">
      <ControlledContainer>
        <CustomInput
          label="Email"
          type="email"
          $invalid={emailNotValid}
          onChange={(event) => handleInputChange('email', event.target.value)}
        />
        <CustomInput
          label="Password"
          type="password"
          $invalid={passwordNotValid}
          onChange={(event) => handleInputChange('password', event.target.value)}
        />
      </ControlledContainer>
      <div className="actions">
        <button type="button" className="text-button">
          Create a new account
        </button>
        <StyledBtn onClick={handleLogin}>Sign In</StyledBtn>
      </div>
    </div>
  );
}
```