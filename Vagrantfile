Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
    config.vm.provider "virtualbox" do |vb|
       vb.gui = false
       vb.memory = "1024"
    end
  config.vm.provision "shell",
    env: {
      "RUN_VERSION" => "2.316.1",
      "RUN_TOKEN" => "ASZ7GHURHP6KYLDUISAGKDTGJZFIW",
      "RUN_REPO" => "kv1382/demo-03-git",
    },
    inline: <<-SHELL
      apt-get update && apt upgrade -y
      runuser -l vagrant -c "mkdir actions-runner && cd actions-runner"
      runuser -l vagrant -c "curl -o actions-runner-linux.tar.gz -L https://github.com/actions/runner/releases/download/v${RUN_VERSION}/actions-runner-linux-x64-${RUN_VERSION}.tar.gz"
      runuser -l vagrant -c "tar xzf ./actions-runner-linux.tar.gz"
      runuser -l vagrant -c "./config.sh --name my_test_runner --labels linux,my_runner --runnergroup default --url https://github.com/${RUN_REPO} --token ${RUN_TOKEN}"
      runuser -l vagrant -c "./run.sh &"
    SHELL
end
