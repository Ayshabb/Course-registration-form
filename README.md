# Course-registration-form
import React, { useState } from "react";
import "./App.css"; // optional if you want styles

function RegistrationForm() {
  const [firstName, setFirstName] = useState("");
  const [lastName, setLastName] = useState("");
  const [email, setEmail] = useState("");
  const [age, setAge] = useState("");
  const [course, setCourse] = useState("");
  const [errors, setErrors] = useState({});
  const [isSubmitted, setIsSubmitted] = useState(false);

  const handleSubmit = (e) => {
    e.preventDefault();

    let formErrors = {};

    // Validation
    if (!firstName.trim()) formErrors.firstName = "First name is required";
    if (!lastName.trim()) formErrors.lastName = "Last name is required";
    if (!email.trim()) {
      formErrors.email = "Email is required";
    } else if (!/\S+@\S+\.\S+/.test(email)) {
      formErrors.email = "Email is invalid";
    }
    if (!age) {
      formErrors.age = "Age is required";
    } else if (Number(age) < 18) {
      formErrors.age = "You must be at least 18";
    }
    if (!course) formErrors.course = "Please select a course";

    setErrors(formErrors);

    if (Object.keys(formErrors).length === 0) {
      setIsSubmitted(true);
      // Clear form
      setFirstName("");
      setLastName("");
      setEmail("");
      setAge("");
      setCourse("");
    } else {
      setIsSubmitted(false);
    }
  };

  return (
    <div className="form-container">
      <h2>Course Registration</h2>
      {isSubmitted && <p className="success">Registration successful!</p>}
      <form onSubmit={handleSubmit}>
        <label>First Name:</label>
        <input
          type="text"
          value={firstName}
          onChange={(e) => setFirstName(e.target.value)}
        />
        {errors.firstName && <p className="error">{errors.firstName}</p>}

        <label>Last Name:</label>
        <input
          type="text"
          value={lastName}
          onChange={(e) => setLastName(e.target.value)}
        />
        {errors.lastName && <p className="error">{errors.lastName}</p>}

        <label>Email:</label>
        <input
          type="email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
        />
        {errors.email && <p className="error">{errors.email}</p>}

        <label>Age:</label>
        <input
          type="number"
          value={age}
          onChange={(e) => setAge(e.target.value)}
        />
        {errors.age && <p className="error">{errors.age}</p>}

        <label>Course:</label>
        <select value={course} onChange={(e) => setCourse(e.target.value)}>
          <option value="">-- Select Course --</option>
          <option value="react">React</option>
          <option value="node">Node.js</option>
          <option value="python">Python</option>
        </select>
        {errors.course && <p className="error">{errors.course}</p>}

        <button type="submit">Register</button>
      </form>
    </div>
  );
}


export default RegistrationForm;
