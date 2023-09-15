![Greenplum](/images/GPDB.jpg)

# An Introduction and Greenplum DB Tutorial using the GPDB Sandbox VM

This repository contains the web based tutorials for Greenplum Database.


# 在本地构建网站预览


## Install Jekyll

```
apt-get install ruby-full build-essential zlib1g-dev
```

```
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

```
gem install jekyll bundler
```

## Build website

```
git clone https://github.com/tuhaihe/gpdb-sandbox.git
```

```
cd gpdb-sandbox
git checkout gh-pages
bundle install
bundle exec jekyll serve
```

Then you can visit：http://127.0.0.1:4000/ to see the local preview.


# Problems and Fix

## No.1

Errors:

```
Conversion error: Jekyll::Converters::Scss encountered an error while converting 'assets/css/style.scss':
                    Invalid US-ASCII character "\xE2" on line 5
..............

/root/gems/gems/jekyll-sass-converter-1.5.2/lib/jekyll/converters/scss.rb:123:in `rescue in convert': Invalid US-ASCII character "\\xE2" on line 5 (Jekyll::Converters::Scss::SyntaxError)
```

Fix:

```
apt-get install -y locales

dpkg-reconfigure locales && \
  locale-gen C.UTF-8 && \
  /usr/sbin/update-locale LANG=C.UTF-8
```

```
echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && \
    locale-gen
```

Then
```
export LC_ALL="C.UTF-8"
export LANG="en_US.UTF-8"
export LANGUAGE="en_US.UTF-8"
```

Last:

```
bundle install
bundle exec jekyll serve
```

## No.2

Errors:

```
/root/gems/gems/jekyll-3.9.3/lib/jekyll/commands/serve/servlet.rb:3:in `require': cannot load such file -- webrick (LoadError)
```

Fix:

```
bundle add webrick # Bundle>1.15
```

Then:

```
bundle install
bundle exec jekyll serve
```