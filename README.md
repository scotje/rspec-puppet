# RSpec tests for your Puppet manifests

This is a work in progress.

## Using
To test that

    sysctl { 'baz'
      value => 'foo',
    }

Will cause the following resource to be in included in catalogue for a host

    exec { 'sysctl/reload':
      command => '/sbin/sysctl -p /etc/sysctl.conf',
    }

We can write the following testcase

    require 'rspec-puppet'

    describe 'sysctl', :type => :define do
      let(:module_path) { '/path/to/puppet/modules' }
      let(:title) { 'baz' }
      let(:params) { { :value => 'foo' } }

      it { should create_exec('sysctl/reload') }
      it { should create_exec('sysctl/reload').with_command("/sbin/sysctl -p /etc/sysctl.conf") }
    end

## TODO

 * Matchers for all the builtin types
 * Move module_path definition to RSpec.configure
 * Override fact values
 * Override node FQDN
