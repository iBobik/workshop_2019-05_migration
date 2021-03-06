## Na co si dát pozor

- Název YML souboru by měl respektovat id migrace, např:


    migrate_plus.migration.user.yml obsahuje migraci s 
    id: user

    migrate_plus.migration.term_article_category.yml obsahuje migraci 
    id:term_article_category


## Drush commands

Zapnout modul

    drush en ws_migration
    
Sledovat stav migrace

    drush ms    
    
Updatovat migraci po změně YML souborů nebo přidání nového YML souboru.
    
    drush cim --partial --source modules/custom/ws_migration/config/install/

    nebo

    drush config-revert migration_config_file_without_yml

    Example:
     
    drush config-revert migrate_plus.migration.term_article_category

Pozor: pro příkaz config-revert musíte mít nainstalovaný modul config_update a config_update_ui.


## Drush příkazy užitečné při testování migrace 
    
    drush migrate:import user --limit=1 --update
    drush mim user --limit=1 --update


## Příkazy pro finální migraci

    drush migrate:import --all --feedback=100
    
    # Někdy nelze migraci spustit najednou, protože dochází paměť.

## Všechny příkazy k migracím
    
    drush | grep migrate
     migrate:                                                                                                                                    
       migrate:status (ms)                        List all migrations with current status.                                                       
       migrate:import (mim)                       Perform one or more migration processes.                                                       
       migrate:rollback (mr)                      Rollback one or more migrations.                                                               
       migrate:stop (mst)                         Stop an active migration operation.                                                            
       migrate:reset-status (mrs)                 Reset a active migration's status to idle.                                                     
       migrate:messages (mmsg)                    View any messages associated with a migration.                                                 
       migrate:fields-source (mfs)                List the fields available for mapping in a source
    
    
## Problémy?

- The "source_....." plugin does not exist.

      drush cr    

- Divné názvy v polích, např. chajahitoclispecastoseslosohithuwrufipr...ticucritrespucrasw
  
  - Zkontrolujte referencovanou migraci. Stává se to, když se zdroj odkazuje na záznam, 
  který ještě není namigrován.     