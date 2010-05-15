ohm-contrib
===========

A collection of drop-in modules for Ohm.

List of modules
---------------
* `Ohm::Boundaries`
* `Ohm::Timestamping`
* `Ohm::ToHash`

Example usage
-------------

    require 'ohm'
    require 'ohm/contrib'
    
    class Post < Ohm::Model
      include Ohm::Timestamping
      include Ohm::ToHash
      include Ohm::Boundaries
      include Ohm::WebValidations
      include Ohm::NumberValidations
        
      attribute :amount
      attribute :url
      attribute :poster_email
      attribute :slug

      def validate
        # from NumberValidations
        assert_decimal :amount

        # or if you want it to be optional
        assert_decimal :amount unless amount.to_s.empty?

        # from WebValidations
        assert_slug  :slug
        assert_url   :url
        assert_email :poster_email
      end
    end

    Post.first
    Post.last
    Post.new.to_hash
    Post.create.to_hash
    Post.create.created_at
    Post.create.updated_at

    # Casting example
    class Product
      include Ohm::Typecast

      attribute :price, :decimal
      attribute :start_of_sale, :time
      attribute :end_of_sale, :time
      attribute :priority, :integer
      attribute :rating, :float
    end

Credits
-------
Thanks to github user gnrfan for the web validations.

Note on Patches/Pull Requests
-----------------------------
* Fork the project.
* Make your feature addition or bug fix.
* Add tests for it. This is important so I don't break it in a
  future version unintentionally.
* Commit, do not mess with rakefile, version, or history.
  (if you want to have your own version, that is fine but bump version in a 
  commit by itself I can ignore when I pull)
* Send me a pull request. Bonus points for topic branches.

Copyright
---------
Copyright (c) 2010 Cyril David. See LICENSE for details.