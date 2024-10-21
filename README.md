### **How to Deploy a Next.js App to SiteGround (Static Export – Next.js 14+)**

This guide explains how to deploy your **Next.js portfolio** or project to **SiteGround** as a **static website** using **Next.js 14+**.

---

### **Step 1: Update `next.config.mjs`**

In **Next.js 14+**, the `next export` command is no longer available. Instead, you need to configure the **`next.config.mjs`** to generate a static site.

1. Open your **`next.config.mjs`**.
2. Ensure the following configuration is added:

   ```javascript
   /** @type {import('next').NextConfig} */
   const nextConfig = {
     reactStrictMode: true,    // Strict mode for debugging
     swcMinify: true,          // Faster builds with SWC minifier
     images: {
       domains: ['sumitake.ca'],  // Allowed domains for images
     },
     output: 'export',         // Export static HTML files
     trailingSlash: true,      // Ensure URLs map to directories correctly
   };

   export default nextConfig;
   ```

---

### **Step 2: Build the Static Site**

1. In your project folder, open a **terminal** (or PowerShell) and run the following commands:

   ```bash
   npm run build
   ```

2. After the build completes, you will see an **`out/` folder** generated in the root of your project. This folder contains your static HTML files.

---

### **Step 3: Upload Files to SiteGround via FileZilla**

1. **Open FileZilla** and log into your **SiteGround FTP** account.
2. On the **right panel** (remote site), navigate to the **`public_html`** folder.
3. On the **left panel** (local site), navigate to the **`out/` folder** in your Next.js project.
4. **Select all files and folders inside the `out/` folder** (e.g., `index.html`, `about.html`, and other assets).
5. **Drag and drop** them into the **`public_html` folder** on the remote site.

---

### **Step 4: Add `.htaccess` for Client-side Routing (Optional)**

If your site uses client-side routing (e.g., `/about`, `/projects`), create an `.htaccess` file to handle the routing:

1. **Create a new file** named **`.htaccess`**.
2. Add the following content:

   ```bash
   Options -Indexes
   RewriteEngine On

   # Redirect all non-file requests to index.html
   RewriteCond %{REQUEST_FILENAME} !-f
   RewriteCond %{REQUEST_FILENAME} !-d
   RewriteRule ^(.*)$ /index.html [L]
   ```

3. **Upload the `.htaccess` file** to the **`public_html` folder** on SiteGround.

---

### **Step 5: Test Your Deployment**

Visit your website at:

```
https://sumitake.ca
```

Verify that:
- All pages load properly.
- Navigation works without any 404 errors.
- Any dynamic routes (like `/projects/[id]`) are handled correctly by your `.htaccess` configuration.

---

### **Summary**

- **Configure `next.config.mjs`** with `output: 'export'`.
- **Run `npm run build`** to generate the static site in the `out/` folder.
- **Upload all files from the `out/` folder** to the `public_html` directory on SiteGround.
- **Optional:** Add an `.htaccess` file to handle client-side routing.
- **Test** your site at `https://sumitake.ca`.

---

This guide ensures your **Next.js 14+ app is deployed as a static website** on SiteGround, with client-side routing handled correctly. Let me know if you have further questions!
