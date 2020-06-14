
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)

set(CMAKE_INCLUDE_CURRENT_DIR ON)


set(libheaders
	qpdf/AES_PDF_native.hh
	qpdf/BitStream.hh
	qpdf/BitWriter.hh
	qpdf/ContentNormalizer.hh
	qpdf/CryptoRandomDataProvider.hh
	qpdf/InsecureRandomDataProvider.hh
	qpdf/MD5.hh
	qpdf/MD5_native.hh
	qpdf/OffsetInputSource.hh
	qpdf/Pl_AES_PDF.hh
	qpdf/Pl_ASCII85Decoder.hh
	qpdf/Pl_ASCIIHexDecoder.hh
	qpdf/Pl_LZWDecoder.hh
	qpdf/Pl_MD5.hh
	qpdf/Pl_PNGFilter.hh
	qpdf/Pl_RC4.hh
	qpdf/Pl_SHA2.hh
	qpdf/Pl_TIFFPredictor.hh
	qpdf/QPDF_Array.hh
	qpdf/QPDF_Bool.hh
	qpdf/qpdf-config.h.in
	#qpdf/QPDFCrypto_gnutls.hh
	qpdf/QPDFCrypto_native.hh
	#qpdf/QPDFCrypto_openssl.hh
	qpdf/QPDF_Dictionary.hh
	qpdf/QPDF_InlineImage.hh
	qpdf/QPDF_Integer.hh
	qpdf/QPDFMatrix.hh
	qpdf/QPDF_Name.hh
	qpdf/QPDF_Null.hh
	qpdf/QPDF_Operator.hh
	qpdf/QPDF_Real.hh
	qpdf/QPDF_Reserved.hh
	qpdf/QPDF_Stream.hh
	qpdf/QPDF_String.hh
	qpdf/RC4.hh
	qpdf/RC4_native.hh
	qpdf/rijndael.h
	qpdf/SecureRandomDataProvider.hh
	qpdf/SHA2_native.hh
	qpdf/SparseOHArray.hh
	sph/sph_sha2.h
	sph/sph_types.h
	
)

# list of source files
set(libsrc
	AES_PDF_native.cc
	BitStream.cc
	BitWriter.cc
	Buffer.cc
	BufferInputSource.cc
	ClosedFileInputSource.cc
	ContentNormalizer.cc
	CryptoRandomDataProvider.cc
	FileInputSource.cc
	InputSource.cc
	InsecureRandomDataProvider.cc
	JSON.cc
	MD5.cc
	MD5_native.cc
	OffsetInputSource.cc
	Pipeline.cc
	Pl_AES_PDF.cc
	Pl_ASCII85Decoder.cc
	Pl_ASCIIHexDecoder.cc
	Pl_Buffer.cc
	Pl_Concatenate.cc
	Pl_Count.cc
	Pl_DCT.cc
	Pl_Discard.cc
	Pl_Flate.cc
	Pl_LZWDecoder.cc
	Pl_MD5.cc
	Pl_PNGFilter.cc
	Pl_QPDFTokenizer.cc
	Pl_RC4.cc
	Pl_RunLength.cc
	Pl_SHA2.cc
	Pl_StdioFile.cc
	Pl_TIFFPredictor.cc
	QPDFAcroFormDocumentHelper.cc
	QPDFAnnotationObjectHelper.cc
	QPDF_Array.cc
	QPDF_Bool.cc
	QPDF.cc
	qpdf-c.cc
	#QPDFCrypto_gnutls.cc
	QPDFCrypto_native.cc
	#QPDFCrypto_openssl.cc
	QPDFCryptoProvider.cc
	QPDF_Dictionary.cc
	QPDF_encryption.cc
	QPDFExc.cc
	QPDFFormFieldObjectHelper.cc
	QPDF_InlineImage.cc
	QPDF_Integer.cc
	QPDF_linearization.cc
	QPDFMatrix.cc
	QPDF_Name.cc
	QPDFNameTreeObjectHelper.cc
	QPDF_Null.cc
	QPDFNumberTreeObjectHelper.cc
	QPDFObject.cc
	QPDFObjectHandle.cc
	QPDFObjGen.cc
	QPDF_Operator.cc
	QPDF_optimization.cc
	QPDFOutlineDocumentHelper.cc
	QPDFOutlineObjectHelper.cc
	QPDFPageDocumentHelper.cc
	QPDFPageLabelDocumentHelper.cc
	QPDFPageObjectHelper.cc
	QPDF_pages.cc
	QPDF_Real.cc
	QPDF_Reserved.cc
	QPDF_Stream.cc
	QPDF_String.cc
	QPDFSystemError.cc
	QPDFTokenizer.cc
	QPDFWriter.cc
	QPDFXRefEntry.cc
	QTC.cc
	QUtil.cc
	RC4.cc
	RC4_native.cc
	sha2.c
	sha2big.c
	rijndael.cc
	SecureRandomDataProvider.cc
	SHA2_native.cc
	SparseOHArray.cc
)

# this is the "object library" target: compiles the sources only once
add_library(libqpdf-obj OBJECT ${libsrc} ${libheaders})
target_include_directories(libqpdf-obj PRIVATE ${JPEG_INCLUDE_DIR})
set_property(TARGET libqpdf-obj PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")

# shared libraries need PIC
set_property(TARGET libqpdf-obj PROPERTY POSITION_INDEPENDENT_CODE 1)

# shared and static libraries built from the same object files
add_library(libqpdf SHARED $<TARGET_OBJECTS:libqpdf-obj>)
target_link_libraries(libqpdf ${JPEG_LIBRARIES} ZLIB::ZLIB)

add_library(libqpdf-static STATIC $<TARGET_OBJECTS:libqpdf-obj>)
