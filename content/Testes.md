Automatizar teste é uma parte essencial de qualquer esforço sério de desenvolvimento de software. A automação facilita a repetição de testes individuais ou teste de suites rapidamente durante o desenvolvimento o que ajuda a garantir que os lançamentos atendam às metas de qualidade e desempenho.




``` user.servicespec
import {vi} from 'vitest'
import {Test, TestingModule} from '@nestjs/testing'
import 'PrismaService' from '../database/prisma.service'
import {UsersService} from './users.service'
import {CreateUserDto} from './dto/create-user.dto'
import {HashingService} from '../hash/hashing.service';

describe("UserService", ()=>{
	let userService: UsersService;
	let prismaService: PrismaService;
	let hashingService: HashingService;
	const createUserDto: CreateUserDto = {
		name: "Tesla",
		email: "tesla@gmail.com",
		password: "123456",
	};
	beforeEach(async ()=>{
		const module:TestingModule = await Test.createTestingModule({
			providers: [
				UsersService,
				{
					provide: PrismaService,
					useValue:{
							user:{
								create: vi.fn(),
								findUnique: vi.fn(),
							},
						}
					}
				},
				{
					provide:HashingService,
					useValue:{
						hash: vi.fn()
					}
				}
			],
		}).compile()
		
		userService = module.get<UsersService>(UsersService);
		prismaService = module.get<PrismaService>(PrismaService);
		hashingService = module.get<HashingService>(HashingService);
		
	});
	
	describe("create", ()=>{
		it("should create new person", async ()=>{
			const passwordHash = "HASHDASENHA";
			const newUser = {
				name: createUserDto.name,
				email: createUserDto.email,
				password: passwordHash
			};
			
			vi.spyOn(prismaService.user, "create").mockResolvedValue(newUser as any);
			vi.spyOn(hashingService, "hash").mockResolvedValue(passwordHash);
			vi.spyOn(prismaService.user, "findUnique").mockResolvedValue(null);
			
			const result = await userService.createUser(createUserDto);
			
			expect(prismaService.user.findUnique).toHaveBeenCalledWith({
				email: createUserDto.email,
			});	expect(hashingService.hash).toHaveBeenCalledWith(createUserDto.password);
			expect(prismaService.user.create),toHaveBeenCalledWith({
				name: createUserDto.name,
				email: createUserDto.email,
				password: passwordHash,
			})
		});
	})
	
})

``` 