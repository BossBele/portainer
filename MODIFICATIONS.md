# Modifications to Portainer Community Edition

**This is a modified version of Portainer Community Edition.**

Original project: [Portainer CE](https://github.com/portainer/portainer)  
License: [zlib License](./LICENSE)

---

## Modifications Made

This fork includes the following changes to enable Business Edition features in Community Edition:

### 1. **RBAC Roles Enabled for Community Edition**

**Files Modified:**
- `app/react/portainer/feature-flags/feature-flags.service.ts` - Changed `RBAC_ROLES` from `Edition.BE` to `Edition.CE`
- `app/react/portainer/users/RolesView/RbacRolesDatatable.tsx` - Updated to dynamically show/hide BE indicator
- `app/portainer/rbac/models/role.js` - Fixed `ID` → `Id` casing for consistency
- `app/portainer/components/accessManagement/porAccessManagementController.js` - Updated role selection logic
- `app/portainer/components/accessManagement/porAccessManagement.html` - Removed role disabling for CE
- `app/portainer/rbac/components/access-viewer/access-viewer.controller.js` - Removed CE restriction

**What Changed:**
- RBAC roles (Administrator, Helpdesk, Standard User, Read-only User) are now available in Community Edition
- Users can be assigned different roles with granular permissions
- Role-based access control is fully functional in CE environments

### 2. **Custom Login Banner Enabled for Community Edition**

**Files Modified:**
- `app/react/portainer/feature-flags/feature-flags.service.ts` - Changed `CUSTOM_LOGIN_BANNER` from `Edition.BE` to `Edition.CE`
- `api/portainer.go` - Added `CustomLoginBanner` field to Settings struct
- `api/http/handler/settings/settings_update.go` - Added banner to update payload
- `api/http/handler/settings/settings_public.go` - Exposed banner in public settings
- `app/portainer/views/auth/authController.js` - Reads banner from settings
- `app/portainer/views/auth/auth.html` - Displays banner on login page

**What Changed:**
- Administrators can now set a custom login banner in Settings → Application
- The banner appears on the login page for all users
- Useful for displaying security notices, terms of use, or custom messages

---

## Why These Changes?

These modifications remove artificial feature restrictions that exist only to differentiate the Business Edition from the Community Edition. The underlying functionality is already present in the codebase but is gated behind edition checks.

**Important Notes:**
- These changes do **not** add new functionality—they only enable existing features
- The backend authorization logic already supports RBAC; we only removed frontend gates
- All changes are minimal and focused on feature flag toggles

---

## Disclaimer

This is **not** the official Portainer Community Edition. This is a modified fork created for personal/organizational use.

- **Original Author:** Portainer.io
- **Modified By:** BossBele
- **Original Repository:** https://github.com/portainer/portainer
- **This Fork:** https://github.com/BossBele/portainer

If you need official support, enterprise features, or want to support the Portainer team, please use the official [Portainer Business Edition](https://www.portainer.io/take-3).

---

## Building and Running

To build this modified version:

```bash
# Build the Docker image
docker build -f build/linux/Dockerfile -t bossbele/portainer-ce-custom:latest .

# Run the container
docker run -d -p 9000:9000 -p 8000:8000 \
  --name portainer \
  --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  bossbele/portainer-ce-custom:latest
```

---

## License

This modified version maintains the original [zlib License](./LICENSE) from Portainer.

As required by the license:
1. ✅ **Origin not misrepresented** - This README clearly states this is based on Portainer's work
2. ✅ **Marked as altered** - All metadata, labels, and documentation identify this as a modified version
3. ✅ **License notice retained** - The original LICENSE file is preserved

---

## Support

This is an **unsupported** community modification. For issues specific to these modifications, please open an issue in this repository. For general Portainer questions, refer to the [official documentation](https://docs.portainer.io).
