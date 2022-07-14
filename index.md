# HackFS 2022 Project BeSync
## Geotemporal Information Coordination


<!-- 1. Install Magic SDK -->
<script src="https://auth.magic.link/sdk"></script>
<script>
/* 2. Initialize Magic Instance */
const magic = new Magic('pk_live_C3F422FED9B82602');


/* 3. Implement Render Function */
const render = async () => {
  let html = '';

  /*
    For this tutorial, our callback route is simply "/callback"
  */
  if (window.location.pathname === '/callback') {
    try {
      /* Complete the "authentication callback" */
      await magic.auth.loginWithCredential();

      /* Get user metadata including email */
      const userMetadata = await magic.user.getMetadata();

      html = `
        <h1>Current user: ${userMetadata.email}</h1>
        <button onclick="handleLogout()">Logout</button>
      `;
    } catch {
      /* In the event of an error, we'll go back to the login page */
      window.location.href = window.location.origin;
    }
  } else {
    const isLoggedIn = await magic.user.isLoggedIn();

    /* Show login form if user is not logged in */
    html = `
      <h1>Please sign up or login</h1>
      <form onsubmit="handleLogin(event)">
        <input type="email" name="email" required="required" placeholder="Enter your email" />
        <button type="submit">Send</button>
      </form>
    `;

    if (isLoggedIn) {
      /* Get user metadata including email */
      const userMetadata = await magic.user.getMetadata();
      html = `
        <h1>Current user: ${userMetadata.email}</h1>
        <button onclick="handleLogout()">Logout</button>
      `;
    }
  }

  document.getElementById('app').innerHTML = html;
};

/* 4. Implement Login Handler */
const handleLogin = async e => {
  e.preventDefault();
  const email = new FormData(e.target).get('email');
  const redirectURI = `${window.location.origin}/callback`; // 👈 This will be our callback URI
  if (email) {
    /* One-liner login 🤯 */
    await magic.auth.loginWithMagicLink({ email, redirectURI }); // 👈 Notice the additional parameter!
    render();
  }
};

/* 5. Implement Logout Handler */
const handleLogout = async () => {
  await magic.user.logout();
  render();
};
</script

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/pensivecyborg/besyncme.io/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
