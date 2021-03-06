# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...



INSTRUCTIONS    _ _ _ __ __ _ _ _

*rails new 'app name'

*Add   gem 'jquery-rails'  to GemFile

*  && Add   group :development, :test do
      gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
      gem 'rspec-rails'
      gem 'launchy'
      gem 'pry'
    end

    group :development do  

    to Gemfile  

* bundle exec rails generate rspec:install (in Terminal)

* Run Rails server in Root dir of project [rails s]

* rake db:create

* rails generate migration [class_name]

* Go into db/migrate/2438403258923095723509[project_name] & Add columns
   EX. t.column(:title, :string) &&  t.timestamps()

*rake db:migrate

*rake db:test:prepare

*create new file in app/models/[class_name].rb and Add
        class [class_name] < ApplicationRecord
        end

* rails g migration create_[class]

* in new migration, set up relationship between Class1 and Class2

* rails g migration add_foreign_key_for_[class2]

* in new migration, set up foreign key relationship between Class1 and Class2

* create a new Model for class in 'app/models/class_name.rb'

* Class2 belongs_to :class1, Class1 has_many :class2

      class Song < ApplicationRecord
        belongs_to :album
      end

      class Album < ApplicationRecord
        has_many :songs
      end

* Add 'models' folder to spec folder and add the album_spec.rb & song_spec.rb

* Add   require 'rails_helper'   to album_spec.rb

* Add
              group :test do
              gem 'shoulda-matchers'
              end                            to GemFile ¡AFTER! all other blocks


* Add                                          
            Shoulda::Matchers.configure do |config|
              config.integrate do |with|
                with.test_framework :rspec
                with.library :rails
              end
            end
                                          to spec/rails_helper.rb


* Add
            require 'rails_helper'

            describe Album do
              it { should have_many(:songs) }
            end                                          
                                            to spec/models/song_spec.rb

* Add
         require 'rails_helper'

         describe Album do
           it { should have_many(:songs) }
         end                                          
                                                                                                                          to spec/models/song_spec.rb


* Add validation for title and length: spec/models/album_spec.rb

  describe(Album) do
    it { should validate_length_of(:name).is_at_most(100) }
  end         

  * Add validation logic in app/models/album.rb

    class Album < ApplicationRecord
      validates :name, presence: true
    end     


*Add  
              before_save(:titleize_survey)

                  private
                  def titleize_survey
                    self.title = self.title.titleize
                  end

                  end                                                            
                                               to app/models/album.rb

*Add
                    Rails.application.routes.draw do
                    root to: 'albums#index'
                    resources :albums do
                    resources :songs
                    end
                    end
                                             to config/routes.rb

* Check routes in terminal      (rake routes)                               

* Add app/controllers/surveys_controller.rb  
    make all the ruby methods
    rename album to survey
    change :genre to :author

* Add layout views for new/edit forms in "apps/views/layouts/_survey_form.html.erb"
