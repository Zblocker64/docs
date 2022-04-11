## akash provider run

run akash provider

```
akash provider run [flags]
```

### Options

```
  -a, --account-number uint                         The account number of the signing account (offline mode only)
      --auth-pem string                             
      --bid-deposit string                          Bid deposit amount (default "50000000uakt")
      --bid-price-cpu-scale uint                    cpu pricing scale in uakt per millicpu
      --bid-price-endpoint-scale uint               endpoint pricing scale in uakt
      --bid-price-memory-scale uint                 memory pricing scale in uakt per megabyte
      --bid-price-script-path string                path to script to run for computing bid price
      --bid-price-script-process-limit uint         limit to the number of scripts run concurrently for bid pricing (default 32)
      --bid-price-script-process-timeout duration   execution timelimit for bid pricing as a duration (default 10s)
      --bid-price-storage-scale uint                storage pricing scale in uakt per megabyte
      --bid-price-strategy string                   Pricing strategy to use (default "scale")
  -b, --broadcast-mode string                       Transaction broadcasting mode (sync|async|block) (default "sync")
      --chain-id string                             The network chain ID
      --cluster-k8s                                 Use Kubernetes cluster
      --cluster-node-port-quantity uint             The number of node ports available on the Kubernetes cluster (default 1)
      --cluster-public-hostname string              The public IP of the Kubernetes cluster
      --cluster-wait-ready-duration duration        The time to wait for the cluster to be available (default 5s)
      --deployment-blocked-hostnames strings        hostnames blocked for deployments
      --deployment-ingress-domain string            
      --deployment-ingress-expose-lb-hosts          
      --deployment-ingress-static-hosts             
      --deployment-network-policies-enabled         Enable network policies (default true)
      --dry-run                                     ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it
      --fees string                                 Fees to pay along with transaction; eg: 10uatom
      --from string                                 Name or address of private key with which to sign
      --gas string                                  gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically (default 200000)
      --gas-adjustment float                        adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored  (default 1)
      --gas-prices string                           Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom)
      --gateway-listen-address string               Gateway listen address (default "0.0.0.0:8443")
      --generate-only                               Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase is not accessible)
  -h, --help                                        help for run
      --inventory-resource-debug-frequency uint     The rate at which to log all inventory resources (default 10)
      --inventory-resource-poll-period duration     The period to poll the cluster inventory (default 5s)
      --k8s-manifest-ns string                      Cluster manifest namespace (default "lease")
      --keyring-backend string                      Select keyring's backend (os|file|kwallet|pass|test) (default "os")
      --keyring-dir string                          The client Keyring directory; if omitted, the default 'home' directory will be used
      --ledger                                      Use a connected Ledger device
      --memo string                                 Memo to send along with transaction
      --offline                                     Offline mode (does not allow any online functionality
      --overcommit-pct-cpu uint                     Percentage of CPU overcommit
      --overcommit-pct-mem uint                     Percentage of memory overcommit
      --overcommit-pct-storage uint                 Percentage of storage overcommit
  -s, --sequence uint                               The sequence number of the signing account (offline mode only)
      --sign-mode string                            Choose sign mode (direct|amino-json), this is an advanced feature
      --timeout-height uint                         Set a block timeout height to prevent the tx from being committed past a certain height
  -y, --yes                                         Skip tx broadcasting prompt confirmation
```

### Options inherited from parent commands

```
      --node string   The node address (default "http://localhost:26657")
```

### SEE ALSO

* [akash provider](akash_provider.md)	 - Akash provider commands

###### Auto generated by spf13/cobra on 18-Feb-2021
