#cisco 

|                                                                                          | Off                     | Green       | Blinking Green           | Amber                      | Blinking Amber                          | Alternating Green/Amber  |
| ---------------------------------------------------------------------------------------- | ----------------------- | ----------- | ------------------------ | -------------------------- | --------------------------------------- | ------------------------ |
| RPS                                                                                      | Off/No RPS              | RPS ready   | RPS up but not available | RPS standby or fault       | Internal PS failed, RPS providing power | N/A                      |
| PoE                                                                                      | Not selected, no issues | Selected    | N/A                      | N/A                        | Not selected, port issues present       | N/A                      |
| When the named mode is selected, the light associated with each physical port indicates: |                         |             |                          |                            |                                         |                          |
| Stat                                                                                     | No link or shutdown     | Link Up     | Activity                 | Port block preventing loop | port blocked preventing loop            | link fault               |
| Duplex                                                                                   | Half-duplex             | Full-duplex | N/A                      | N/A                        | N/A                                     | N/A                      |
| Speed                                                                                    | 10Mbps                  | 100Mbps     | 1000Mbps                 | N/A                        | N/A                                     | N/A                      |
| PoE                                                                                      | PoE off                 | PoE on      | N/A                      | PoE disabled               | PoE off due to fault                    | PoE denied (over budget) |


