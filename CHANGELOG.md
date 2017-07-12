# Changelog

All notable changes to [Twist API](https://developer.twistapp.com) will be
documented in this file. The format is based
on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/).

Keep in mind we just expose the major version as a resource. Instead of using
`https://api.twistapp.com/api/v2.0.1`, it will be
`https://api.twistapp.com/api/v2`. All minor and patch versions are maintained
just for documentation purposes as it
follows [Semantic Versioning](http://semver.org/spec/v2.0.0.html) and must not
break between minor patches.

## [Unreleased]

## [2.0.1] - 2017-07-11

### Changed

- `id` is not needed for users#getone anymore. It returns the user related to
  the current token in case `id` is not present
