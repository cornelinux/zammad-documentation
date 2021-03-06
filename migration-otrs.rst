from OTRS
*********

Via Browser
===========

After installing Zammad, open http://localhost:3000 with your browser and follow the installation wizard.
From there you're able to start migration from OTRS.

See the Video @ http://days.zammad.org/features/migrator

Via command line
================

If you miss this at the beginning or you want to re-import again you have to use the command line at the moment.

* Install Znuny4OTRS-Repo, which is a dependency for the OTRS migration plugin

  * OTRS 5:

    * http://portal.znuny.com/api/addon_repos/public/615/latest

  * OTRS 4:

    * http://portal.znuny.com/api/addon_repos/public/309/latest

* Install OTRS migration plugin on OTRS

  * OTRS 5:

    * https://portal.znuny.com/api/addon_repos/public/617/latest

  * OTRS 4:

    * https://portal.znuny.com/api/addon_repos/public/383/latest

  * OTRS 3.1 - 3.3:

    * https://portal.znuny.com/api/addon_repos/public/287/latest

* Stop all Zammad processes and switch Zammad to import mode (no events are fired - e. g. notifications, sending emails, ...)

  You need to run the following commands in the zammad context. So start

::

 zammad run rails c

 Setting.set('import_otrs_endpoint', 'http://xxx/otrs/public.pl?Action=ZammadMigrator')
 Setting.set('import_otrs_endpoint_key', 'xxx')
 Setting.set('import_mode', true)
 Import::OTRS.start

After the import is done switch Zammad back to non import mode and mark the system initialization as done

::

 Setting.set('import_mode', false)
 Setting.set('system_init_done', true)

Start all Zammad processes again. Done.

**Note: Currently only passwords of OTRS >= 3.3 can be reused in Zammad! Passwords that were stored in another format than the default SHA2 are not possible to use. Users then have to use the password reset procedure.**

