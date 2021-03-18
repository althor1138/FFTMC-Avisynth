function fftmc(clip input, int "sigma", int "beta", int "mthresh", int "blocksize", int "overlap", float "sharpen", clip "auxclip" )
{

s=Defined(sigma)
sigma=s ? sigma : 2.0

b=Defined(beta)
beta=b ? beta : 1.0

m=Defined(mthresh)
mthresh=m ? mthresh : 120

bs=Defined(blocksize)
blocksize=bs ? blocksize : 32

o=Defined(overlap)
overlap=o ? overlap : 16

sh=Defined(sharpen)
sharpen=sh ? sharpen : 2

aux=Defined(auxclip)
auxclip=aux ? auxclip : input


prefilt=auxclip
super = MSuper(input,pel=1)
superfilt=MSuper(prefilt,pel=1)
backward_vectors = MAnalyse(superfilt, isb = true,blksize=blocksize,truemotion=false)
forward_vectors = MAnalyse(superfilt, isb = false,blksize=blocksize,truemotion=false)
forward_compensation = Mcompensate(input,super, forward_vectors, thsad=mthresh)
backward_compensation = Mcompensate(input,super, backward_vectors, thsad=mthresh)
interleave(forward_compensation, input, backward_compensation)
fft3dfilter(sigma=sigma,beta=beta,plane=4,bw=blocksize,bh=blocksize,bt=3,ow=overlap,oh=overlap,kratio=2.0,sharpen=sharpen,scutoff=0.3,svr=1.0,smin=4.0,smax=20.0,measure=true,interlaced=false,wintype=0,pframe=0,px=0,py=0,pshow=false,pcutoff=0.1,pfactor=0,degrid=1.0,dehalo=0,hr=2.0,ht=50,ncpu=2)
selectevery(3,1)
}
