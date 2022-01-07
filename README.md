## Some code for Arduino Mega2560
1. 8 Byte double to 4 byte float
```
float conv(uint8_t *dn) {
    union {
        float f;
        uint8_t b[4];
    } fn;

    int expd = ((dn[7] & 127) << 4) + ((dn[6] & 240) >> 4);
    int expf = expd ? (expd - 1024) + 128 : 0;
    fn.b[3] = (dn[7] & 128) + (expf >> 1);
    fn.b[2] = ((expf & 1) << 7) + ((dn[6] & 15) << 3) + ((dn[5] & 0xe0) >> 5);
    fn.b[1] = ((dn[5] & 0x1f) << 3) + ((dn[4] & 0xe0) >> 5);
    fn.b[0] = ((dn[4] & 0x1f) << 3) + ((dn[3] & 0xe0) >> 5);

    return fn.f;
}
```
