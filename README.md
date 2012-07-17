# Paperclip::Qiniu

storage [paperclip](https://github.com/thoughtbot/paperclip/) attachments to http://qiniutek.com

example project: https://github.com/lidaobing/paperclip-qiniu-example

example site: http://stark-cloud-4321.herokuapp.com/

## Usage

0. confirm you are working on a rails app

1. add following line to `Gemfile`

```
gem 'paperclip'
gem 'paperclip-qiniu'
```

2. edit your `config/application.rb`

```
module PaperclipQiniuExample
  class Application < Rails::Application
    # ....
    config.paperclip_defaults = {:storage => :qiniu,
      :qiniu_credentials => {
        :access_key => ENV['QINIU_ACCESS_KEY'] || raise("set env QINIU_ACCESS_KEY"),
        :secret_key => ENV['QINIU_SECRET_KEY'] || raise("set env QINIU_SECRET_KEY")
      },
      :bucket => "paperclip-qiniu-example",
      :use_timestamp => false
    }
  end
end
```

3. add a model like this

```
class Image < ActiveRecord::Base
  attr_accessible :file
  has_attached_file :file, :styles => { :medium => "300x300>", :thumb => "100x100>" }
  validates :file, :attachment_presence => true
end
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
