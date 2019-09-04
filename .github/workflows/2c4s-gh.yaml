workflow "Terraform" {
  resolves = "terraform-plan"
  on = "pull_request"
  env = {
    TF_ACTION_WORKING_DIR = "./src"
  }
}

action "filter-to-pr-open-synced" {
  uses = "actions/bin/filter@master"
  args = "action 'opened|synchronize'"
}

action "terraform-fmt" {
  uses = "hashicorp/terraform-github-actions/fmt@v0.3.6
  needs = "filter-to-pr-open-synced"
}

action "terraform-init" {
  uses = "hashicorp/terraform-github-actions/init@v0.3.6"
  needs = "terraform-fmt"
  secrets = ["GITHUB_TOKEN"]
}

action "terraform-validate" {
  uses = "hashicorp/terraform-github-actions/validate@v0.3.6"
  needs = "terraform-init"
  secrets = ["GITHUB_TOKEN"]
}

action "terraform-plan" {
  uses = "hashicorp/terraform-github-actions/plan@v0.3.6"
  needs = "terraform-validate"
  secrets = ["GITHUB_TOKEN"]
  env = {
    TF_ACTION_WORKSPACE = "default"
  }
}
