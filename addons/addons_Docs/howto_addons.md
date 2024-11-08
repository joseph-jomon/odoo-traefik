To add custom Odoo add-ons (modules), you’ll place them in the `addons` directory in your project’s folder structure, as defined in the `docker-compose.yml` file. Here’s how to set it up:

### Folder Structure

Update your project’s folder structure as follows:
```
odoo_project/
├── docker-compose.yml
├── config/
│   └── odoo.conf              # Odoo configuration file (with addons_path specified)
├── addons/                    # Custom addons folder (put your modules here)
│   ├── custom_module1/        # Example custom module
│   └── custom_module2/
├── odoo_pg_pass               # PostgreSQL password file
```

### Steps to Add Add-Ons

1. **Place Modules in the `addons` Directory**:
   - Add your custom Odoo modules inside the `addons/` directory (e.g., `addons/custom_module1/`, `addons/custom_module2/`).
   - Each module should follow the standard Odoo module structure, with at minimum an `__init__.py` and `__manifest__.py`.

2. **Update `addons_path` in `odoo.conf`**:
   - The `addons_path` in `odoo.conf` already includes `/mnt/extra-addons`, which maps to the `addons/` directory in your project folder through the `docker-compose.yml` file:
     ```ini
     addons_path = /mnt/extra-addons
     ```
   - No changes are needed here since `docker-compose.yml` mounts `./addons` to `/mnt/extra-addons` in the container, making your custom modules accessible.

3. **Restart Docker Compose**:
   - Run the following to apply changes and load the add-ons:
     ```bash
     docker-compose down
     docker-compose up -d
     ```
   - This restarts the services, and Odoo should now recognize the add-ons placed in the `addons/` folder.

4. **Verify in Odoo**:
   - Log in to your Odoo instance, navigate to **Apps**, and click on **Update App List**.
   - Your custom modules should now be visible in the list of available apps, ready for installation.

### Summary of Changes Needed
- Place your custom modules in the `addons/` folder.
- Ensure `addons_path = /mnt/extra-addons` in `odoo.conf`.
- Restart the services with Docker Compose to load the new modules.

With this setup, Odoo will read from both its default add-ons and any custom modules in your `addons` directory.