# libiconv_msvc
```
//#pragma  comment(lib,"libiconv.lib")
#ifdef __cplusplus
extern "C" {
#endif
extern  __declspec(dllimport) void* libiconv_open(const char* tocode, const char* fromcode);
extern  __declspec(dllimport) size_t libiconv(void* cd, char* * inbuf, unsigned int *inbytesleft, char* * outbuf, unsigned int *outbytesleft);
extern  __declspec(dllimport) int libiconv_close(void* cd);
extern	__declspec(dllimport) void libiconvlist(int(*do_one) (unsigned int namescount,const char * const * names,void* data),void* data);
#ifdef __cplusplus
}
#endif

//example:
int covert(char *tocode, char *fromcode, char *inbuf, size_t inbyteslen, char *output, size_t outbyteslen)
{
	char **pinbuf = &inbuf;
	char **poutput = &output;
	void* handel = libiconv_open(tocode,fromcode);
	if ((int)handel == -1)
	{
		return -1;
	}
	memset(output,0,outbyteslen);
	if (libiconv(handel, pinbuf, &inbyteslen, poutput, &outbyteslen)) return -1;
	libiconv_close(handel);
	return 0;
}

int main()
{
char *input = "绝地求生";
size_t len = strlen(input);
char output[256] = {0};
covert("UTF-8", "GBK", input, len, output, 256);
return 0;
}
```
