# IceChain



There could be a slower Workchain that would store long term archives, let’s call it an IceChain. Such an IceСhain would operate exactly like the DriveChain with some modifications. Since the DriveChain is a Virtual Drive blockchain and the data should be readily available in the current state of the art, the use of Zero Knowledge Proofs (ZKP) may not be practical. Yet in the IceChain where validators can store the files in a long-term Glacier type of Storage (such as Tapes etc.) the access time does not play such a role as the user is expecting to get the file with potentially significant delays. This opens a possibility to use non-interactive ZKPs with no trusted setup for data sampling.

The sampling would include constructing a ZKP for a different random number of chunks for each verification whose delay could be set to minutes. That would render the possibility of data corruption in the IceChain to virtually zero. The proofs would be verified by Everscale Verifiers periodically and would contain everything required to blame if the data is not available or corrupted. When the ZKP reached the state of technology that would enable them to produce the proofs at the high rate, they could replace the verification mechanism on the DriveChain as well.
