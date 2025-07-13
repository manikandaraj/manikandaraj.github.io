---
title: "Contact Me"
date: 2025-03-01T01:30:00-05:00
lastmod: 2025-03-01T01:30:00-05:00
#menu: "main"
#weight: 50
---

# Get in Touch

Please fill out the form below to contact me.

<form id="contactForm">
  <div>
    <label for="name">Name *</label><br>
    <input type="text" id="name" name="name" required />
  </div>
  <br>
  <div>
    <label for="email">Email *</label><br>
    <input type="email" id="email" name="email" required />
  </div>
  <br>
  <div>
    <label for="subject">Subject *</label><br>
    <input type="text" id="subject" name="subject" required />
  </div>
  <br>
  <div>
    <label for="message">Message *</label><br>
    <textarea id="message" name="message" rows="5" required></textarea>
  </div>
  <br>
  <button type="submit">Send Message</button>
</form>

<div id="formMessage" style="margin-top:20px;color:green;"></div>

<script>
  // Listen for form submission
  document.getElementById("contactForm").addEventListener("submit", async function(e) {
    e.preventDefault(); // Prevent default form submission

    // Clear previous messages
    const formMessage = document.getElementById("formMessage");
    formMessage.textContent = "";
    formMessage.style.color = "green";

    // Gather form field values
    const name = document.getElementById("name").value.trim();
    const email = document.getElementById("email").value.trim();
    const subject = document.getElementById("subject").value.trim();
    const message = document.getElementById("message").value.trim();

    // Basic validations
    if (!name) {
      formMessage.style.color = "red";
      formMessage.textContent = "Please enter your name.";
      return;
    }
    if (!email) {
      formMessage.style.color = "red";
      formMessage.textContent = "Please enter your email.";
      return;
    }
    // Simple email regex check
    const emailRegex = /^[^\\s@]+@[^\\s@]+\\.[^\\s@]+$/;
    if (!emailRegex.test(email)) {
      formMessage.style.color = "red";
      formMessage.textContent = "Please enter a valid email address.";
      return;
    }
    if (!subject) {
      formMessage.style.color = "red";
      formMessage.textContent = "Please enter a subject.";
      return;
    }
    if (!message) {
      formMessage.style.color = "red";
      formMessage.textContent = "Please enter a message.";
      return;
    }

    // Prepare data to send
    const formData = {
      name: name,
      email: email,
      subject: subject,
      message: message
    };

    try {
      // Make an asynchronous POST request to the API
      const response = await fetch("https://api.manikandaraj.com/blog/contact-me", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(formData)
      });

      if (response.ok) {
        // If API returns a 200 OK, reset the form and display a success message.
        document.getElementById("contactForm").reset();
        formMessage.style.color = "green";
        formMessage.textContent = "Thank you! Your contact has been made.";
      } else {
        // If the response status is not 200, show an error message.
        formMessage.style.color = "red";
        formMessage.textContent = "There was an error sending your message. Please try again.";
      }
    } catch (error) {
      console.error("Error:", error);
      formMessage.style.color = "red";
      formMessage.textContent = "There was an error sending your message. Please try again.";
    }
  });
</script>
