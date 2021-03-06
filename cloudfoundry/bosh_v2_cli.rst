
::

  add-blob               Add blob                                           https://bosh.io/docs/cli-v2#add-blob
  alias-env              Alias environment to save URL and CA certificate   https://bosh.io/docs/cli-v2#alias-env
  attach-disk            Attaches disk to an instance                       https://bosh.io/docs/cli-v2#attach-disk
  blobs                  List blobs                                         https://bosh.io/docs/cli-v2#blobs
  cancel-task            Cancel task at its next checkpoint                 https://bosh.io/docs/cli-v2#cancel-task (aliases: ct)
  clean-up               Clean up releases, stemcells, disks, etc.          https://bosh.io/docs/cli-v2#clean-up
  cloud-check            Cloud consistency check and interactive repair     https://bosh.io/docs/cli-v2#cloud-check (aliases: cck, cloudcheck)
  cloud-config           Show current cloud config                          https://bosh.io/docs/cli-v2#cloud-config (aliases: cc)
  config                 Show current config for either ID or both type and name https://bosh.io/docs/cli-v2#config (aliases: c)
  configs                List configs                                       https://bosh.io/docs/cli-v2#configs (aliases: cs)
  cpi-config             Show current CPI config                            https://bosh.io/docs/cli-v2#cpi-config
  create-env             Create or update BOSH environment                  https://bosh.io/docs/cli-v2#create-env
  create-release         Create release                                     https://bosh.io/docs/cli-v2#create-release (aliases: cr)
  delete-config          Delete config                                      https://bosh.io/docs/cli-v2#delete-config (aliases: dc)
  delete-deployment      Delete deployment                                  https://bosh.io/docs/cli-v2#delete-deployment (aliases: deld)
  delete-disk            Delete disk                                        https://bosh.io/docs/cli-v2#delete-disk
  delete-env             Delete BOSH environment                            https://bosh.io/docs/cli-v2#delete-env
  delete-release         Delete release                                     https://bosh.io/docs/cli-v2#delete-release (aliases: delr)
  delete-snapshot        Delete snapshot                                    https://bosh.io/docs/cli-v2#delete-snapshot
  delete-snapshots       Delete all snapshots in a deployment               https://bosh.io/docs/cli-v2#delete-snapshots
  delete-stemcell        Delete stemcell                                    https://bosh.io/docs/cli-v2#delete-stemcell (aliases: dels)
  delete-vm              Delete VM                                          https://bosh.io/docs/cli-v2#delete-vm
  deploy                 Update deployment                                  https://bosh.io/docs/cli-v2#deploy (aliases: d)
  deployment             Show deployment information                        https://bosh.io/docs/cli-v2#deployment (aliases: dep)
  deployments            List deployments                                   https://bosh.io/docs/cli-v2#deployments (aliases: ds, deps)
  diff-config            Diff two configs by ID                             https://bosh.io/docs/cli-v2#diff-config
  disks                  List disks                                         https://bosh.io/docs/cli-v2#disks
  environment            Show environment                                   https://bosh.io/docs/cli-v2#environment (aliases: env)
  environments           List environments                                  https://bosh.io/docs/cli-v2#environments (aliases: envs)
  errands                List errands                                       https://bosh.io/docs/cli-v2#errands (aliases: es)
  event                  Show event details                                 https://bosh.io/docs/cli-v2#event
  events                 List events                                        https://bosh.io/docs/cli-v2#events
  export-release         Export the compiled release to a tarball           https://bosh.io/docs/cli-v2#export-release
  finalize-release       Create final release from dev release tarball      https://bosh.io/docs/cli-v2#finalize-release
  generate-job           Generate job                                       https://bosh.io/docs/cli-v2#generate-job
  generate-package       Generate package                                   https://bosh.io/docs/cli-v2#generate-package
  help                   Show this help message                             https://bosh.io/docs/cli-v2#help
  ignore                 Ignore an instance                                 https://bosh.io/docs/cli-v2#ignore
  init-release           Initialize release                                 https://bosh.io/docs/cli-v2#init-release
  inspect-release        List release contents such as jobs                 https://bosh.io/docs/cli-v2#inspect-release
  instances              List all instances in a deployment                 https://bosh.io/docs/cli-v2#instances (aliases: is)
  interpolate            Interpolates variables into a manifest             https://bosh.io/docs/cli-v2#interpolate (aliases: int)
  locks                  List current locks                                 https://bosh.io/docs/cli-v2#locks
  log-in                 Log in                                             https://bosh.io/docs/cli-v2#log-in (aliases: l, login)
  log-out                Log out                                            https://bosh.io/docs/cli-v2#log-out (aliases: logout)
  logs                   Fetch logs from instance(s)                        https://bosh.io/docs/cli-v2#logs
  manifest               Show deployment manifest                           https://bosh.io/docs/cli-v2#manifest (aliases: man)
  orphan-disk            Orphan disk                                        https://bosh.io/docs/cli-v2#orphan-disk
  recreate               Recreate instance(s)                               https://bosh.io/docs/cli-v2#recreate
  releases               List releases                                      https://bosh.io/docs/cli-v2#releases (aliases: rs)
  remove-blob            Remove blob                                        https://bosh.io/docs/cli-v2#remove-blob
  repack-stemcell        Repack stemcell                                    https://bosh.io/docs/cli-v2#repack-stemcell
  reset-release          Reset release                                      https://bosh.io/docs/cli-v2#reset-release
  restart                Restart instance(s)                                https://bosh.io/docs/cli-v2#restart
  run-errand             Run errand                                         https://bosh.io/docs/cli-v2#run-errand
  runtime-config         Show current runtime config                        https://bosh.io/docs/cli-v2#runtime-config (aliases: rc)
  scp                    SCP to/from instance(s)                            https://bosh.io/docs/cli-v2#scp
  snapshots              List snapshots                                     https://bosh.io/docs/cli-v2#snapshots
  ssh                    SSH into instance(s)                               https://bosh.io/docs/cli-v2#ssh
  start                  Start instance(s)                                  https://bosh.io/docs/cli-v2#start
  stemcells              List stemcells                                     https://bosh.io/docs/cli-v2#stemcells (aliases: ss)
  stop                   Stop instance(s)                                   https://bosh.io/docs/cli-v2#stop
  sync-blobs             Sync blobs                                         https://bosh.io/docs/cli-v2#sync-blobs
  take-snapshot          Take snapshot                                      https://bosh.io/docs/cli-v2#take-snapshot
  task                   Show task status and start tracking its output     https://bosh.io/docs/cli-v2#task (aliases: t)
  tasks                  List running or recent tasks                       https://bosh.io/docs/cli-v2#tasks (aliases: ts)
  unignore               Unignore an instance                               https://bosh.io/docs/cli-v2#unignore
  update-cloud-config    Update current cloud config                        https://bosh.io/docs/cli-v2#update-cloud-config (aliases: ucc)
  update-config          Update config                                      https://bosh.io/docs/cli-v2#update-config (aliases: uc)
  update-cpi-config      Update current CPI config                          https://bosh.io/docs/cli-v2#update-cpi-config
  update-resurrection    Enable/disable resurrection                        https://bosh.io/docs/cli-v2#update-resurrection
  update-runtime-config  Update current runtime config                      https://bosh.io/docs/cli-v2#update-runtime-config (aliases: urc)
  upload-blobs           Upload blobs                                       https://bosh.io/docs/cli-v2#upload-blobs
  upload-release         Upload release                                     https://bosh.io/docs/cli-v2#upload-release (aliases: ur)
  upload-stemcell        Upload stemcell                                    https://bosh.io/docs/cli-v2#upload-stemcell (aliases: us)
  variables              List variables                                     https://bosh.io/docs/cli-v2#variables (aliases: vars)
  vendor-package         Vendor package                                     https://bosh.io/docs/cli-v2#vendor-package
  vms                    List all VMs in all deployments                    https://bosh.io/docs/cli-v2#vms
