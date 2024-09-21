<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prakash, Contact Me!</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #FFFCF2;
            color: #333;
            margin: 0;
            padding: 0;
        }

        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
            background-color: #FFFFFF;
            padding: 20px;
            border-radius: 10px;
            max-width: 100%;
            margin: 10px auto;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
        }

        .header {
            display: flex;
            align-items: left;
            justify-content: space-between;
            width: 100%;
            margin-bottom: 20px;
        }

        .header .details {
            flex: 1;
        }

        .profile-pic {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            object-fit: cover;
            margin-left: 20px;
        }

        h1,
        h2 {
            color: #003366;
            font-size: 1.8em;
            margin: 0;
        }

        p {
            font-size: 1em;
            line-height: 1.5;
            margin: 5px 0;
        }

        a {
            color: #1DA1F2;
            text-decoration: none;
        }

        a:hover {
            text-decoration: underline;
        }

        hr {
            border: none;
            border-top: 1px solid #DDDDDD;
            margin: 10px 0;
        }

        .quote {
            font-style: italic;
            color: #555;
            margin-top: 20px;
            padding: 15px;
            background-color: #FFFCF2;
            border-left: 5px solid #003366;
        }

        ul {
            list-style-type: disc;
            margin-left: 20px;
        }

        section {
            transition: transform 0.3s ease, box-shadow 0.3s ease, background-color 0.3s ease;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            background-color: #FFFFFF;
        }

        section:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
            background-color: #7ef9ff;
        }

        .no-popup {
            transition: none;
            box-shadow: none;
            background-color: inherit;
            transform: none;
        }

        .social-media {
            display: flex;
            justify-content: left;
            align-items: center;
            margin-top: 20px;
        }

        .social-media a {
            margin: 0 10px;
        }

        .social-media img {
            width: 35px;
            height: 35px;
            border-radius: 10px;
            transition: transform 0.3s, box-shadow 0.3s;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .social-media img:hover {
            transform: translateY(-3px) scale(1.1);
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
        }

        @media (max-width: 600px) {
            h1,
            h2 {
                font-size: 1.5em;
            }

            p,
            ul li {
                font-size: 0.9em;
            }

            .container {
                padding: 15px;
            }

            .header {
                flex-direction: column;
                align-items: center;
            }

            .profile-pic {
                margin-left: 0;
                margin-top: 10px;
                width: 120px;
                height: 120px;
            }

            .social-media img {
                width: 35px;
                height: 35px;
            }
        }

        /* Contact Form Styles */
        label {
            display: block;
            margin-bottom: 10px;
            font-weight: bold;
        }

        input,
        textarea,
        button {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 16px;
        }

        button {
            width: auto;
            padding: 8px 16px;
            background-color: #000;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 14px;
        }

        button:hover {
            background-color: #333;
        }

        .required:after {
            content: "*";
            color: red;
            margin-left: 5px;
        }
    </style>
</head>

<body>
    <div class="container">
        <!-- Header with Details and Profile Picture -->
        <div class="header">
            <div class="details">
                <h1>Chandra Prakash Sharma</h1>
                <h2>Web Developer</h2>
                <p><strong>Email:</strong> <a href="mailto:contact@cpsharma.com">contact@cpsharma.com</a></p>
                <p><strong>Location:</strong> Prayagraj, India</p>

                <!-- Social Media Section -->
                <div class="social-media">
                    <a href="https://www.google.com" target="_blank">
                        <img src="https://github.com/prakashsharma19/prakash/blob/main/11244080_x_twitter_elon%20musk_twitter%20new%20logo_icon.png?raw=true"
                            alt="Twitter Logo">
                    </a>
                    <a href="https://www.google.com" target="_blank">
                        <img src="https://github.com/prakashsharma19/prakash/blob/main/5296499_fb_facebook_facebook%20logo_icon.png?raw=true"
                            alt="Facebook Logo">
                    </a>
                    <a href="https://www.google.com" target="_blank">
                        <img src="https://github.com/prakashsharma19/prakash/blob/main/1696902_apps_media_quora_social_icon.png?raw=true"
                            alt="Quora Logo">
                    </a>
                    <a href="https://www.linkedin.com/in/prakash-sharma-31a80428a?original_referer=https%3A%2F%2Fwww.google%2Ecom%2F&originalSubdomain=in"
                        target="_blank">
                        <img src="https://github.com/prakashsharma19/prakash/blob/main/5296501_linkedin_network_linkedin%20logo_icon.png?raw=true"
                            alt="LinkedIn Logo">
                    </a>
                    <a href="https://www.google.com" target="_blank">
                        <img src="https://github.com/prakashsharma19/prakash/blob/main/5296765_camera_instagram_instagram%20logo_icon.png?raw=true"
                            alt="Instagram Logo">
                    </a>
                </div>
            </div>
            <img src="https://github.com/prakashsharma19/prakash/blob/main/my_image-removebg-preview.png?raw=true"
                alt="Profile Picture" class="profile-pic">
        </div>

        <hr>

        <div class="content">
            <!-- About Me Section -->
            <section>
                <h2>About Me</h2>
                <ul>
                    <li><strong>Highest Education:</strong> Masters of Business Administration (MBA) in Marketing and
                        Information Technology from AKTU</li>
                    <li><strong>Interests:</strong> Website Development, Coding, AI, Open-Source Projects, Prompt
                        Engineering, Psychology</li>
                    <li><strong>Skills:</strong> Problem Solving, Programming, English Proficiency (CEFR B2), Web
                        Development, Digital Marketing. More details available on <a
                            href="https://in.linkedin.com/in/prakash-sharma-31a80428a?original_referer=https%3A%2F%2Fwww.google.com%2F">LinkedIn</a>.
                    </li>
                    <li><strong>Currently Learning:</strong> Python, Data Science, Cloud Computing, Prompt Engineering,
                        etc.</li>
                    <li><strong>Looking to Collaborate On:</strong> Innovative projects related to AI and sustainability
                    </li>
                </ul>
            </section>
            <hr>

            <!-- Contact Form -->
            <section>
                <h2>Contact Me</h2>
                <form action="https://formspree.io/f/xgvwjkqz" method="POST">
                    <label for="name" class="required">Your Name</label>
                    <input type="text" id="name" name="name" required>

                    <label for="email" class="required">Your Email</label>
                    <input type="email" id="email" name="email" required>

                    <label for="message" class="required">Your Message</label>
                    <textarea id="message" name="message" rows="4" required></textarea>

                    <button type="submit">Submit</button>
                </form>
            </section>

        </div>
    </div>
</body>

</html>
