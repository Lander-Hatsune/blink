create_conn:
1. Allocate a struct of connection IO.
2. Use a random number of length LOCAL_CONN_ID_LEN to
   create a connection ID.
3. Create a quiche connection.

recv_cb:
1. Try receiving info using conns->sock
2. Extract quiche header info from buf
4. If no connection exists, confirm header info:
   Check quiche version and try negotiation;
   If our peer is stateless, generate a new token and send a retry packet.
   If the token is still invalid, just discard the packet.
And create a new connection.
5. Receive info using the quiche connection.
6. After the quiche connection is established, send and receive stream info.

main:
1. Get host and port from cmd.And get address info.
2. Create a socket.
3. Configure the quiche protocol.
