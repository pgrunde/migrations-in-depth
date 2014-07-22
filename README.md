# Migrations

## Migrations alter a database schema over time in a consistent and repeatable way.

## Migrations are time stamped and create a new or revised version of your database: YYYYMMDDHHMMSS

## Create Migration Files
	
	$ rake db:create_migration
	
	# in Rails
	$ rails generate migration ...
	
	
	$ rake db:create_migration CreateUsersTable
	20140722101534_create_users_table.rb


### Different migration commands:

	create_table
	add_column
	add_index
	add_reference
	add_timestamps
	
	drop_table
	remove_column
	remove_index
	remove_reference
	remove_timestamps
	
	rename_table
	rename_column

### YYYYMMDDHHMMSS_create_users_table.rb
### 20140722101534_create_users_table.rb
	    
    class CreateUsers < ActiveRecord::Migration
		def up
    		create_table :users do |t|
      			t.string :name
      			t.string :email      			
 
      			t.timestamps
    		end
    	end
    	
    	def down
    		drop_table :users 
    	end
    end
    
    class CreateUsers < ActiveRecord::Migration
		def change
    		create_table :users do |t|
      			t.string :name
      			t.string :email
 
      			t.timestamps
    		end
    	end
    end


	
### YYYYMMDDHHMMSS_add_address_to_users.rb

	class AddAddressToUsers < ActiveRecord::Migration
		def change
			add_column :users, :address, :string
		end
	end
	

	
## $ rake db:migrate

* runs all migration files that have not been run before
* the migrations run in order of their "timestamp"

## $ rake db:rollback

* rolls back (undoes) the most recent migration

## $ rake db:rollback STEP=3

* rolls back the 3 most recent migrations


## Three different databases: development, test, production

### Development:

	$ rake db:migrate

### Test:

	$ RACK_ENV=test rake db:migrate
	
	# in Rails:
	$ rake db:test:prepare

### Production - Heroku:

	$ heroku run rake db:migrate
	
